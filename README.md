# Internship Project Report

## Project Title:
**Image Colorization with Artistic Style Transfer**

**Student Name:** Mehkaan Anjum  
**Course:** BCA  

---

## 1. Project Overview
This project demonstrates a simple approach to **image colorization** combined with **artistic style transfer**.  
It allows users to upload a **grayscale image**, generate a **colorized version**, and apply **artistic styles** (Warm, Cool, Sketch) using Python libraries.  

The project is designed for internship submission and provides a **user-friendly GUI** for demonstration purposes.

---

## 2. Objectives
- Convert grayscale images into colorized images.  
- Apply artistic styles (Warm, Cool, Sketch) to enhance the visual appearance.  
- Provide a graphical interface for easy user interaction.  
- Save the final styled image for demonstration and submission.

---

## 3. Tools and Libraries
- **Python 3.x**  
- **Pillow (PIL):** for image manipulation  
- **OpenCV:** for image processing and artistic filters  
- **NumPy:** for array operations  
- **Gradio:** for creating an interactive GUI  

---

## 4. Methodology
The project follows these steps:

1. **Image Upload:**  
   Users upload a grayscale image through the Gradio GUI.

2. **Grayscale Conversion:**  
   The uploaded image is converted to grayscale using Pillow (`.convert("L")`) to ensure proper input for colorization.

3. **Colorization:**  
   A simple colorization function generates simulated RGB colors:
   - **Red channel:** grayscale intensity  
   - **Green channel:** inverse of grayscale  
   - **Blue channel:** Gaussian blurred grayscale  

4. **Artistic Style Transfer:**  
   The colorized image is processed to apply the selected style:
   - **Warm Style:** Pinkish tone using OpenCV colormap (`COLORMAP_PINK`)  
   - **Cool Style:** Bluish tone using OpenCV colormap (`COLORMAP_WINTER`)  
   - **Sketch:** Converts the image to a sketch-like outline using grayscale inversion and Gaussian blur  

5. **Output Generation:**  
   The final styled image is displayed in the GUI and saved locally as `final_output.jpg`.

---

## 5. GUI Interface
The project uses **Gradio** to provide an interactive interface with:
- **Image upload input** (supports PIL images)  
- **Dropdown menu** to select artistic style  
- **Outputs:** Grayscale image, colorized image, final styled image  

The GUI makes it easy for users to see the transformation in real-time.

---

## 6. Observations and Limitations
- **Colorization is simulated**; it is not AI-based and produces basic color effects.  
- Artistic styles are created using **OpenCV colormaps and simple filters**, so results are not fully photo-realistic.  
- Works best with **clear and simple images** such as faces, objects, or landscapes.  
- Fully executable in **Google Colab or a local Python environment**.

---

## 7. Future Enhancements
- Integrate **AI-based colorization models** for realistic color outputs.  
- Add additional **artistic styles** using neural style transfer.  
- Enhance GUI with **download options** and **error handling** for unsupported files.

---

## 8. Conclusion
This project successfully demonstrates a **basic image colorization pipeline** with **artistic style effects**.  
It is **safe, executable, and suitable for internship submission**, and provides a visually engaging way to present grayscale-to-color image transformation.

---

## 9. Author
**Mehkaan Anjum**  
BCA Student
