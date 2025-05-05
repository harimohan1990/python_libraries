# python_libraries 

📊 Data Analysis & Science
Pandas – Data manipulation and analysis

NumPy – Numerical computing

SciPy – Scientific computing

Matplotlib – Plotting and visualization

Seaborn – Statistical data visualization

🤖 Machine Learning & AI
Scikit-learn – ML algorithms

TensorFlow – Deep learning

Keras – High-level deep learning API (uses TensorFlow backend)

PyTorch – Deep learning framework

XGBoost – Optimized gradient boosting

🧪 Web Scraping
BeautifulSoup – HTML and XML parsing

Scrapy – Web scraping framework

Requests – HTTP library

🌐 Web Development
Flask – Lightweight web framework

Django – Full-stack web framework

FastAPI – High-performance API framework

🧮 Automation & Scripting
Selenium – Web automation

PyAutoGUI – GUI automation

Schedule – Job scheduling

🧠 Natural Language Processing
NLTK – NLP toolkit

spaCy – Industrial-strength NLP

TextBlob – Simplified NLP

🗃️ Databases
SQLAlchemy – SQL toolkit & ORM

PyMongo – MongoDB integration

SQLite3 – Built-in support for SQLite

🧪 Testing
unittest – Built-in testing framework

pytest – Advanced testing framework

mock – Mocking objects in tests

🎮 Game Development
Pygame – 2D game development

Ursina – Beginner-friendly 3D engine

Panda3D – Full 3D game engine

Godot (via GDScript/Python API) – Game scripting

💰 Finance & Quantitative Analysis
yfinance – Fetch financial data from Yahoo Finance

QuantLib – Quantitative finance tools

TA-Lib – Technical analysis indicators

ccxt – Crypto exchange trading library

🧠 AI/ML in Healthcare
MONAI – Deep learning for medical imaging

PyRadiomics – Radiomic feature extraction

SimpleITK – Medical image analysis

🗺️ Geospatial & Maps
Geopandas – Geospatial data analysis

Folium – Map visualizations using Leaflet.js

Shapely – Geometry operations

Rasterio – Working with geospatial raster data

🎨 Image Processing & Computer Vision
OpenCV – Image/video processing

Pillow (PIL) – Image manipulation

scikit-image – Image processing

imageio – Read/write images

🧪 Scientific Computing & Engineering
SymPy – Symbolic math

Astropy – Astronomy-focused tools

Biopython – Bioinformatics

OpenMM – Molecular simulation

🧑‍🎨 GUI Development
Tkinter – Built-in GUI framework

PyQt – Powerful cross-platform GUI

Kivy – Touch-friendly GUI for mobile/desktop

Dear PyGui – Fast, GPU-accelerated GUI


🧠 Basic Chatbot Stack
NLP: spaCy or ChatterBot

Transformer-based AI: transformers (e.g., GPT-2)

Web server: Flask or FastAPI

Voice (optional): speech_recognition, pyttsx3


example of You're building a React + FastAPI + ChatGPT API chatbot. Here's a clean structure to get you started:

Perfect! You're building a **React + FastAPI + ChatGPT API** chatbot. Here's a clean structure to get you started:

---

### 📁 Project Structure

```
chatbot-app/
├── backend/
│   └── main.py
├── frontend/
│   └── (React app)
```

---

### ✅ Backend (`main.py` with FastAPI)

```python
from fastapi import FastAPI, Request
from fastapi.middleware.cors import CORSMiddleware
import openai
import os

openai.api_key = os.getenv("OPENAI_API_KEY")

app = FastAPI()
app.add_middleware(CORSMiddleware, allow_origins=["*"], allow_methods=["*"], allow_headers=["*"])

@app.post("/chat")
async def chat(request: Request):
    data = await request.json()
    user_msg = data.get("message", "")

    response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=[{"role": "user", "content": user_msg}]
    )
    reply = response["choices"][0]["message"]["content"]
    return {"reply": reply}
```

Run backend:

```bash
uvicorn main:app --reload
```

---

### ✅ Frontend (React `App.js`)

```jsx
import { useState } from "react";

function App() {
  const [messages, setMessages] = useState([]);
  const [input, setInput] = useState("");

  const sendMessage = async () => {
    const res = await fetch("http://localhost:8000/chat", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ message: input })
    });
    const data = await res.json();
    setMessages([...messages, { role: "user", text: input }, { role: "bot", text: data.reply }]);
    setInput("");
  };

  return (
    <div style={{ padding: 20 }}>
      <h2>ChatGPT Bot</h2>
      {messages.map((m, i) => (
        <p key={i}><strong>{m.role}:</strong> {m.text}</p>
      ))}
      <input value={input} onChange={e => setInput(e.target.value)} />
      <button onClick={sendMessage}>Send</button>
    </div>
  );
}

export default App;
```

---

### 🌐 Enable CORS and Env

* Create `.env` in `backend/`:

  ```env
  OPENAI_API_KEY=your_openai_key_here
  ```

* Use `python-dotenv` if needed for loading `.env`:

  ```bash
  pip install python-dotenv
  ```

