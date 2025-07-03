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
## 🎨 Compressor.js
```
//Components/Compressor.js
import React,
{
    useState, useEffect
} from 'react';
import {
    Navbar, Card,
    Spinner, Modal,
    Button
} from 'react-bootstrap';
import { FontAwesomeIcon }
    from '@fortawesome/react-fontawesome';
import {
    faImage, faDownload,
    faUpload, faImage as faImagePlaceholder,
    faQuestionCircle,
    faHistory
} from '@fortawesome/free-solid-svg-icons';
import './Compressor.css';
import { compress }
    from 'image-conversion';
function CompressorComp() {
    const [compressedLink, setCompressedLink] = useState('');
    const [originalImage, setOriginalImage] = useState(null);
    const [originalLink, setOriginalLink] = useState('');
    const [uploadImage, setUploadImage] = useState(false);
    const [outputFileName, setOutputFileName] = useState('');
    const [compressionQuality, setCompressionQuality] = useState(0.8);
    const [originalSize, setOriginalSize] = useState(0);
    const [compressedSize, setCompressedSize] = useState(0);
    const [isCompressed, setIsCompressed] = useState(false);
    const [compressionInProgress, setCompressionInProgress] = useState(false);
    const [loading, setLoading] = useState(false);
    const [showHelp, setShowHelp] = useState(false);
    const [showHistory, setShowHistory] = useState(false);
    const [compressedHistory, setCompressedHistory] = useState([]);
    const [showCompressedImage, setShowCompressedImage] = useState(false);
    const [modalShow, setModalShow] = useState(false);

    useEffect(() => {
        if (originalImage) {
            setCompressedLink('');
            setCompressedSize(0);
            setIsCompressed(false);
            setShowCompressedImage(false);
        }
    }, [originalImage]);

    async function uploadLink(event) {
        const imageFile = event.target.files[0];
        setOriginalLink(URL.createObjectURL(imageFile));
        setOriginalImage(imageFile);
        setOutputFileName(imageFile.name);
        setUploadImage(true);
        setOriginalSize(imageFile.size);
    }
    async function compressImage() {
        if (!originalImage) {
            alert('Please upload an image first.');
            return;
        }
        try {
            setCompressionInProgress(true);
            setShowCompressedImage(false);
            setLoading(true);
            const compressedImage =
                await compress(originalImage, {
                    quality: compressionQuality,
                    width: 800,
                    height: 800,
                });
            setCompressedLink(URL.createObjectURL(compressedImage));
            setCompressedSize(compressedImage.size);
            setIsCompressed(true);
            setCompressedHistory(
                [
                    ...compressedHistory,
                    {
                        link: compressedLink,
                        name: outputFileName
                    }
                ]);
            setTimeout(
                () => {
                    setLoading(false);
                    setShowCompressedImage(true);
                }, 2000);
        } catch (error) {
            console.error('Image compression failed:', error);
            alert('Image compression failed. Please try again.');
        } finally {
            setCompressionInProgress(false);
        }
    }
    function resetApp() {
        setOriginalLink('');
        setOriginalImage(null);
        setUploadImage(false);
        setOutputFileName('');
        setCompressionQuality(0.8);
        setOriginalSize(0);
        setCompressedSize(0);
        setIsCompressed(false);
        setCompressedLink('');
        setShowCompressedImage(false);
    }
    function toggleHelp() {
        setShowHelp(!showHelp);
    }
    function toggleHistory() {
        setShowHistory(!showHistory);
    }
    return (
        <div className="mainContainer">
            <Navbar className="navbar justify-content-between"
                bg="lig" variant="dark">
                <div>
                    <Navbar.Brand className="navbar-content">
                        <center>
                            {/* <FontAwesomeIcon icon={faImage}
                                className="icon" /> */}
                            Akhu Image Compressor
                        </center>
                    </Navbar.Brand>
                </div>
                <div className="navbar-actions">
                    <FontAwesomeIcon icon={faQuestionCircle}
                        className="help-icon" onClick={toggleHelp} />
                    <FontAwesomeIcon icon={faHistory}
                        className="history-icon" onClick={toggleHistory} />
                </div>
            </Navbar>
            {showHelp && (
                <div className="help-container">
                    <p>Instructions:</p>
                    <ul>
                        <li>
                            Upload an image using
                            the "Upload a file" button.
                        </li>
                        <li>
                            Adjust the compression
                            quality using the slider.
                        </li>
                        <li>
                            Press the "Compress" button
                            to start the compression.
                        </li>
                        <li>
                            Download the compressed image
                            using the "Download" button.
                        </li>
                    </ul>
                </div>
            )}
            {showHistory && (
                <div className="history-container">
                    <p>Compressed History:</p>
                    <ul>
                        {
                            compressedHistory.map(
                                (item, index) => (
                                    <li key={index}>
                                        <a href={item.link}
                                            download={item.name}>
                                            {item.name}
                                        </a>
                                    </li>
                                ))
                        }
                    </ul>
                </div>
            )}
            <div className="row mt-5">
                <div className="col-xl-3 col-lg-3 
                col-md-12 col-sm-12">
                    {uploadImage ? (
                        <Card.Img className="image"
                            variant="top" src={originalLink}
                            alt="Original Image" />
                    ) : (
                        <Card.Img className="uploadCard"
                            variant="top" src={faUpload} alt="" />
                    )}
                    <div className="d-flex justify-content-center 
                    upload-btn-wrapper">
                        <label htmlFor="uploadBtn"
                            className="btn btn-primary">
                            <FontAwesomeIcon icon={faUpload}
                                className="icon" />
                            Upload a file
                        </label>
                        <input
                            type="file"
                            id="uploadBtn"
                            accept="image/*"
                            className="mt-2 btn btn-primary w-75"
                            onChange={(event) => uploadLink(event)} />
                    </div>
                </div>
                <div
                    className="col-xl-6 col-lg-6 
                        col-md-12 col-sm-12 
                        d-flex justify-content-center 
                        align-items-baseline">
                    <div>
                        {outputFileName ? (
                            <div>
                                <label htmlFor="qualitySlider">
                                    Compression Quality:
                                </label>
                                <input
                                    id="qualitySlider"
                                    type="range"
                                    min="0.1"
                                    max="1"
                                    step="0.1"
                                    value={compressionQuality}
                                    onChange={
                                        (event) =>
                                            setCompressionQuality(
                                                parseFloat(event.target.value)
                                            )
                                    }
                                />
                                <div className="text-center">
                                    Original Size:
                                    {
                                        Math.round(originalSize / 1024)
                                    } KB
                                    <br />
                                    Compressed Size:
                                    {
                                        Math.round(compressedSize / 1024)
                                    } KB
                                </div>
                                <div className="text-center">
                                    {isCompressed &&
                                        !compressionInProgress && (
                                            <div className="text-success 
                                            compressed-message">
                                                Image compressed successfully!
                                            </div>
                                        )}
                                    {
                                        compressionInProgress &&
                                        <div className="text-info">
                                            Compressing image...
                                        </div>
                                    }
                                </div>
                                <div className="button-container">
                                    {loading ? (
                                        <div className="text-info">
                                            Loading...
                                        </div>
                                    ) : (
                                        <button type="button"
                                            className="btn btn-success"
                                            onClick={compressImage}>
                                            <FontAwesomeIcon icon={faImage}
                                                className="icon" />
                                            Compress
                                        </button>
                                    )}
                                    <button type="button"
                                        className="btn btn-danger ml-3"
                                        onClick={resetApp}>
                                        Reset
                                    </button>
                                </div>
                            </div>
                        ) : (
                            <></>
                        )}
                    </div>
                </div>
                <div className="col-xl-3 col-lg-3 col-md-12 col-sm-12">
                    {showCompressedImage ? (
                        <div>
                            <Card.Img
                                className="image"
                                variant="top"
                                src={compressedLink}
                                alt="Compressed Image"
                                onClick={() => setModalShow(true)}
                                style={{ cursor: 'pointer' }}
                            />
                            <a href={compressedLink}
                                download={outputFileName}
                                className="mt-2 btn btn-success 
                                w-75 download-btn">
                                <FontAwesomeIcon icon={faDownload}
                                    className="icon" />
                                Download
                            </a>
                            <Modal show={modalShow}
                                onHide={
                                    () =>
                                        setModalShow(false)
                                } size="lg">
                                <Modal.Body className="text-center">
                                    <Card.Img className="image"
                                        variant="top" src={compressedLink}
                                        alt="Compressed Image" />
                                </Modal.Body>
                                <Modal.Footer>
                                    <Button variant="secondary"
                                        onClick={
                                            () => setModalShow(false)
                                        }>
                                        Close
                                    </Button>
                                </Modal.Footer>
                            </Modal>
                        </div>
                    ) : (
                        <div className="d-flex align-items-center 
                        justify-content-center">
                            {
                                compressionInProgress &&
                                <Spinner animation="border" variant="primary" />
                            }
                            {
                                !uploadImage &&
                                !compressionInProgress && (
                                    <FontAwesomeIcon icon={faImagePlaceholder}
                                        className="icon" size="3x" />
                                )
                            }
                        </div>
                    )}
                </div>
            </div>
        </div>
    );
}
export default CompressorComp;
```

## 🎨 App.js
```
//App.js
import React from 'react';
import './App.css';
import CompressorComp 
    from "./Components/Compressor";
import 'bootstrap/dist/css/bootstrap.css';
function App() {
    return (
        <CompressorComp />
    );
}
export default App;
```
