# 🖼️ Image Compressor using ReactJS**
Live link : https://compress-ur-image.netlify.app/**

An interactive feature-rich **Image Compressor** built with **ReactJS**, enabling users to upload images, control compression quality via a slider, and download compressed images. It also includes instructions and history navigation for enhanced UX.

## 🚀 Features
- 📤 Upload images (only valid image files)
- 🎚️ Adjust compression quality using a slider
- 📥 Download the compressed image
- 📚 Access compression history and instructions
- 🔄 Reset and re-upload functionality
- 📱 Responsive design with React-Bootstrap

---

## 📦 Tech Stack
- ReactJS (Function Components)
- Bootstrap 5
- React-Bootstrap
- Font Awesome
- image-conversion library

---

## 📁 Folder Setup
Bootstrapped using `create-react-app`. Organized components with separate CSS.

**Key dependencies in `package.json`:**
```json
"react": "^18.2.0",
"bootstrap": "^5.3.2",
"react-bootstrap": "^2.9.1",
"image-conversion": "^2.1.1",
"@fortawesome/free-solid-svg-icons": "^6.4.2",
"@fortawesome/react-fontawesome": "^0.2.0"
```

---

## 💻 How to Run

```bash
# Clone the repo
git clone https://github.com/your-username/image-compressor.git
cd image-compressor

# Install dependencies
npm install

# Start the server
npm start
```

Then visit: [http://localhost:3000](http://localhost:3000)

---

## 📂 Example Files

### 🧠 App Logic and UI

> The app uses components like NavBar, Button, Modal, Spinner, Slider, and validation logic to ensure proper compression behavior.  
> For full implementation, refer to:

- `App.js`
- `Compressor.js`
- `Compressor.css`

---

## 🎨 Sample Styles – Compressor.css

```css
.mainContainer {
  text-align: center;
}
.navbar {
  background-color: #fff78b;
  padding: 20px;
  box-shadow: 0 4px 8px rgba(233, 12, 12, 0.2);
}
.navbar-content {
  color: green;
  font-weight: bold;
  font-size: 24px;
  text-transform: uppercase;
  display: flex;
  justify-content: center;
  align-items: center;
}
.upload-btn-wrapper {
  position: relative;
  display: inline-block;
  overflow: hidden;
}
.upload-btn-wrapper input[type="file"] {
  font-size: 100px;
  position: absolute;
  left: 0;
  top: 0;
  opacity: 0;
}
.btn {
  padding: 10px 20px;
  font-weight: bold;
  border-radius: 8px;
  transition: transform 0.2s;
}
.btn:hover {
  transform: scale(1.05);
}
.btn-reset {
  background-color: #e74c3c;
}
.btn-reset:hover {
  background-color: #c0392b;
}
.compressed-message {
  font-size: 24px;
  color: #2ecc71;
}
.compressed-message:hover {
  color: #27ae60;
}
```

---

## 📅 Last Updated
**25 Jul, 2024**
