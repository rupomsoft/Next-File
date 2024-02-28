Next-File is a lightweight npm package tailored for file management within Next.js applications. It simplifies the process of uploading files to your Next.js server and provides an easy-to-use interface for deleting files when they are no longer needed. With seamless integration into Next.js projects, this package offers robust functionality to handle file uploads and deletions efficiently, enhancing the development experience for Next.js developers.

```javascript
npm i next-file
// Using yarn 
yarn add next-file
```
![next-file.png](next-file.png)
Features:
- File Upload: Easily upload files to your Next.js server with minimal configuration.
- File Deletion: Delete files from your server effortlessly when they are no longer required.
- Supported Formats: Supports a wide range of file formats including images, documents, and more.
- Error Handling: Provides comprehensive error handling to ensure smooth file management operations.
- Lightweight: Designed to be lightweight and unobtrusive, minimizing overhead and optimizing performance.
- Next.js Integration: Seamlessly integrates into Next.js projects, maintaining compatibility with the Next.js ecosystem.


#### Example File Upload Form Next.js Route 
```javascript
export async function POST(req,res) {
    try{
        let result=await Upload(req,"files",['jpg','png','pdf'])
        return NextResponse.json({status:"success",data:result})
    }
    catch (e) {
        return  NextResponse.json({status:"fail",data:e})
    }
}
```

#### Example File Delete Form Next.js Route
```javascript
export async function DELETE(req,res) {
    try{
        const filePath = './public/files/1709098593107_demo.png';
        let result=await deleteFile(filePath)
        return NextResponse.json({status:"success",data:result})
    }
    catch (e) {
        return  NextResponse.json({status:"fail",data:e})
    }
}
```

#### Example Multipart Form Data Request Using Axios From React Component

```javascript
import React, { useState } from 'react';
import axios from 'axios';

const FileUploadForm = () => {
  const [selectedFile, setSelectedFile] = useState(null);

  const handleFileChange = (event) => {
    setSelectedFile(event.target.files[0]);
  };

  const handleSubmit = async (event) => {
    event.preventDefault();

    if (!selectedFile) {
      alert('Please select a file');
      return;
    }

    try {
      const formData = new FormData();
      formData.append('file', selectedFile);

      const response = await axios.post('http://localhost:3000/upload', formData, {
        headers: {
          'Content-Type': 'multipart/form-data'
        }
      });

      console.log('File uploaded successfully:', response.data);
    } catch (error) {
      console.error('Error uploading file:', error);
    }
  };

  return (
    <div>
      <h2>File Upload</h2>
      <form onSubmit={handleSubmit}>
        <input type="file" onChange={handleFileChange} />
        <button type="submit">Upload</button>
      </form>
    </div>
  );
};

export default FileUploadForm;

```
#### Example Multipart Form Data Request Using Fetch API From React Component

```javascript
import React, { useState } from 'react';

const FileUploadForm = () => {
  const [selectedFile, setSelectedFile] = useState(null);

  const handleFileChange = (event) => {
    setSelectedFile(event.target.files[0]);
  };

  const handleSubmit = async (event) => {
    event.preventDefault();

    if (!selectedFile) {
      alert('Please select a file');
      return;
    }

    try {
      const formData = new FormData();
      formData.append('file', selectedFile);

      const response = await fetch('http://localhost:3000/upload', {
        method: 'POST',
        body: formData
      });

      if (!response.ok) {
        throw new Error(`HTTP error! status: ${response.status}`);
      }

      const data = await response.json();
      console.log('File uploaded successfully:', data);
    } catch (error) {
      console.error('Error uploading file:', error);
    }
  };

  return (
    <div>
      <h2>File Upload</h2>
      <form onSubmit={handleSubmit}>
        <input type="file" onChange={handleFileChange} />
        <button type="submit">Upload</button>
      </form>
    </div>
  );
};

export default FileUploadForm;

```


MIT License

Copyright (c) [2024] [RABBIL HASAN]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.



