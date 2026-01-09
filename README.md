# Image-colorization-
My Frist project 
# =====================================
# INSTALL REQUIRED LIBRARIES (COLAB)
# =====================================
!pip install -q tensorflow tensorflow-hub pillow opencv-python matplotlib

# =====================================
# IMPORTS
# =====================================
import tensorflow as tf
import tensorflow_hub as hub
import numpy as np
import cv2
from PIL import Image
import matplotlib.pyplot as plt
from google.colab import files

# =====================================
# LOAD NEURAL STYLE TRANSFER MODEL
# =====================================
print("Loading Neural Style Transfer model...")
nst_model = hub.load(
    "https://tfhub.dev/google/magenta/arbitrary-image-stylization-v1-256/2"
)
print("Model loaded successfully")

# =====================================
# IMAGE LOADING FUNCTION (SAFE FOR COLAB)
# =====================================
def load_image_pil(image_path, size=(256, 256)):
    img = Image.open(image_path).convert("RGB")
    img = img.resize(size)
    img = np.array(img).astype(np.float32) / 255.0
    img = img[np.newaxis, :]
    return img

# =====================================
# COLORIZATION FUNCTION (BASIC)
# =====================================
def colorize_image(image_path):
    """
    NOTE:
    This is pseudo-colorization.
    Real projects use GAN-based models (future scope).
    """
    img = Image.open(image_path).convert("L")   # grayscale
    img = np.array(img)
    img = cv2.cvtColor(img, cv2.COLOR_GRAY2BGR)
    colorized = cv2.applyColorMap(img, cv2.COLORMAP_TURBO)
    return colorized

# =====================================
# UPLOAD IMAGES
# =====================================
print("Upload CONTENT image (grayscale preferred)")
content_upload = files.upload()
content_path = list(content_upload.keys())[0]

print("Upload STYLE image (painting/art)")
style_upload = files.upload()
style_path = list(style_upload.keys())[0]

# =====================================
# COLORIZE CONTENT IMAGE
# =====================================
colorized_img = colorize_image(content_path)

# Save temporary colorized image
cv2.imwrite("colorized_temp.jpg", colorized_img)

# =====================================
# PREPARE IMAGES FOR NST
# =====================================
content_img = load_image_pil("colorized_temp.jpg")
style_img = load_image_pil(style_path)

# =====================================
# APPLY NEURAL STYLE TRANSFER
# =====================================
print("Applying Artistic Style Transfer...")
stylized_img = nst_model(
    tf.constant(content_img),
    tf.constant(style_img)
)[0]

# =====================================
# DISPLAY RESULTS
# =====================================
plt.figure(figsize=(18,6))

plt.subplot(1,3,1)
plt.title("Original Content Image")
plt.imshow(Image.open(content_path))
plt.axis("off")

plt.subplot(1,3,2)
plt.title("Colorized Image")
plt.imshow(cv2.cvtColor(colorized_img, cv2.COLOR_BGR2RGB))
plt.axis("off")

plt.subplot(1,3,3)
plt.title("Artistic Style Transfer Output")
plt.imshow(stylized_img.numpy()[0])
plt.axis("off")

plt.show()
