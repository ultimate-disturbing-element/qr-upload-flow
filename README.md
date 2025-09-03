# QR Upload Flow

A lightweight SDK that allows clients to **capture or upload images**, **send them to any backend service**, and **fetch uploaded files** with ease.
Supports **custom upload APIs**, **polling for new files**, and **camera integration**.

---

## 📦 Installation

```bash
npm install ultimate-disturbing-element/qr-upload-flow
# or
yarn add ultimate-disturbing-element/qr-upload-flow
```

## 🚀 Usage

```bash
import QrUpload from "qr-upload-flow";

const sdk = new QrUpload();

const config = {
  qrUrl: {
    frontendUrl: "https://your-frontend.com",
    sdkRoute: "/qr-upload",  // sdk path to open the camera preview
  },

  fetchApi: {
    url: "https://your-backend.com/api", // GET
    headers: {
      // Optional headers
    },
    responseKey: "data.files", // Path to files in API response
  },

  uploadApi: {
    url: "https://your-backend.com/api", // POST
    headers: {
      // Optional headers
    },
    body: {
      // Optional request body
    },
    fileKey: "file",
    onUploadImageSuccess: (uploadedFiles) => {
      console.log("Uploaded files:", uploadedFiles);
    },
  },

  polling: {
    enablePolling: true,
    pollingInterval: 10000,  //10sec
    onPollingStart: () => console.log("Polling started"),
    onPollingStop: () => console.log("Polling stopped"),
    onPollingError: (err) => console.error("Polling error:", err),
    onNewFiles: (files) => console.log("New files received:", files),
  },

  logoUrl: "https://your-logo.com/logo.png",
  autoStartCamera: true,
  imageConfig: {
    multiPhoto: false,
    maxImages: 1,
    allowedMimeTypes: ["image/jpeg", "image/png", "image/webp"],
  },
};

```


```bash
sdk.init(config)
```

## 🔎 Overview of Core Modules

### 📷 generateQRCode
Generates a QR code that can be scanned by clients to **capture or upload images** using their device camera or gallery.  
Useful for cross-device flows where one device scans and uploads, while another fetches the results.

---

### 📂 fetchApi
Handles fetching already uploaded files from your backend.  
- Configure the `url` and `responseKey` to match your API.  
- Returns the list of files so you can display them in your app.  

---

### ⬆️ uploadApi
Uploads images directly to your backend.  
- Specify the `url` and `fileKey`.  
- Supports optional headers, body data, and authentication.  
- Triggers `onUploadImageSuccess` callback once files are uploaded successfully.  

---

### 🔄 polling
Automatically checks your backend for **new uploaded files** at regular intervals.  
- Controlled by `enablePolling` and `pollingInterval`.  
- Comes with callbacks like `onPollingStart`, `onPollingStop`, `onPollingError`, and `onNewFiles`.  
- Ideal for scenarios where new files may appear without refreshing the app.  




## 📖 SDK Documentation

Initializes the SDK with the provided configuration.

Configuration Options

### qrUrl
| Key         | Type   | Description                                |
| ----------- | ------ | ------------------------------------------ |
| frontendUrl | string | URL to open for QR-based capture/upload    |
| sdkRoute    | string | Route used by the SDK for handling uploads |

### fetchApi
| Key         | Type   | Description                                 |
| ----------- | ------ | ------------------------------------------- |
| url         | string | Endpoint to fetch uploaded files            |
| headers     | object | Optional headers (e.g., authentication)     |
| responseKey | string | Key in API response where files are located |

### uploadApi
| Key                  | Type     | Description                                 |
| -------------------- | -------- | ------------------------------------------- |
| url                  | string   | Endpoint for uploading images               |
| headers              | object   | Headers for authentication or metadata      |
| body                 | object   | Extra form data sent with the upload        |
| fileKey              | string   | Form field name for files                   |
| onUploadImageSuccess | function | Callback executed after a successful upload |

### polling
| Key             | Type     | Description                            |
| --------------- | -------- | -------------------------------------- |
| enablePolling   | boolean  | Enable or disable polling              |
| pollingInterval | number   | Interval in milliseconds between polls |
| onPollingStart  | function | Called when polling begins             |
| onPollingStop   | function | Called when polling stops              |
| onPollingError  | function | Called if polling fails                |
| onNewFiles      | function | Called with newly fetched files        |


### imageConfig
| Key              | Type      | Description                          |
| ---------------- | --------- | ------------------------------------ |
| multiPhoto       | boolean   | Allow multiple photos in one session |
| maxImages        | number    | Maximum number of images allowed     |
| allowedMimeTypes | string\[] | Allowed image MIME types             |


## ✅ Features

- Works with any backend  
- Framework-agnostic (**React, Vue, Angular, Vanilla JS**)  
- Supports **camera capture, upload, and file fetching**  
- Built-in **polling support** for auto-refreshing uploads  
- Lightweight & fully customizable  

