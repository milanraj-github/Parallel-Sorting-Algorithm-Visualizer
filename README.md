# Parallel Sorting Algorithm Visualizer ⚡📊

[![React](https://img.shields.io/badge/React-19.2-61DAFB?style=flat-square&logo=react&logoColor=black)](https://react.dev/)
[![Vite](https://img.shields.io/badge/Vite-8.3-646CFF?style=flat-square&logo=vite&logoColor=white)](https://vitejs.dev/)
[![Python](https://img.shields.io/badge/Python-3.11%2B-3776AB?style=flat-square&logo=python&logoColor=white)](https://python.org/)
[![Flask](https://img.shields.io/badge/Flask-3.1-000000?style=flat-square&logo=flask&logoColor=white)](https://flask.palletsprojects.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg?style=flat-square)](LICENSE)

An academic-grade, full-stack web application designed for the **B.E. Computer Science & Engineering** curriculum subject **Parallel Computing**.

The visualizer pairs step-by-step interactive algorithm simulations with **genuine OS-level multi-core multiprocessing** in Python, live microsecond performance benchmarking, speedup scaling curves, and a clean **Dark/Light theme** UI.

---

## 🌟 Key Highlights

- ⚡ **True Multiprocessing Concurrency**: Leverages Python `multiprocessing.Pool` across 2, 4, or 8 physical/logical CPU cores—not just simulated web workers.
- 🎨 **Theme System**: Seamless toggle between a developer **Dark Mode** and crisp **Light Mode** with local persistence.
- 🔬 **Academic Correctness Verification**: 3-point mathematical validation (Sorted Order, Algorithmic Equivalence, Element Conservation).
- 📈 **Performance Benchmarking**: Microsecond-precision timing using `time.perf_counter()`, interactive Recharts speedup curves, and Amdahl's Law analysis.
- 🕹️ **Interactive Playground**: Real-time step controls (Play, Pause, Resume, Reset, Speed Slider) across 6 algorithms.

---

## 🚀 Live Demo & Visual Overview

| Sorting Playground | Parallel Multiprocessing Lane |
|:---:|:---:|
| Interactive step-by-step state animations with comparing, swapping, pivot, and sorted highlights. | Visualizes balanced chunking ($k = \lfloor N / P \rfloor$), concurrent worker lanes, and K-way tree reduction. |

---

## 🧠 Algorithms Supported & Complexities

| Algorithm | Best Case | Average Case | Worst Case | Space Complexity | Parallelizable |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Bubble Sort** | $\mathcal{O}(n)$ | $\mathcal{O}(n^2)$ | $\mathcal{O}(n^2)$ | $\mathcal{O}(1)$ | ❌ Sequential |
| **Selection Sort** | $\mathcal{O}(n^2)$ | $\mathcal{O}(n^2)$ | $\mathcal{O}(n^2)$ | $\mathcal{O}(1)$ | ❌ Sequential |
| **Insertion Sort** | $\mathcal{O}(n)$ | $\mathcal{O}(n^2)$ | $\mathcal{O}(n^2)$ | $\mathcal{O}(1)$ | ❌ Sequential |
| **Merge Sort** | $\mathcal{O}(n \log n)$ | $\mathcal{O}(n \log n)$ | $\mathcal{O}(n \log n)$ | $\mathcal{O}(n)$ | ⚠️ Recursive |
| **Quick Sort** | $\mathcal{O}(n \log n)$ | $\mathcal{O}(n \log n)$ | $\mathcal{O}(n^2)$ | $\mathcal{O}(\log n)$ | ⚠️ Recursive |
| **Parallel Merge Sort** | $\mathcal{O}(\frac{n}{P} \log \frac{n}{P})$ | $\mathcal{O}(\frac{n}{P} \log \frac{n}{P} + n \log P)$ | $\mathcal{O}(\frac{n}{P} \log \frac{n}{P} + n \log P)$ | $\mathcal{O}(n)$ | ✅ True Multiprocessing |

---

## 📐 Formal Parallel Computing Formulas

### 1. Speedup ($S$)
$$\text{Speedup } (S) = \frac{T_{\text{sequential}}}{T_{\text{parallel}}}$$
*Quantifies the acceleration achieved by distributing work across $P$ concurrent processor cores.*

### 2. Parallel Efficiency ($E$)
$$\text{Efficiency } (E) = \left( \frac{S}{P} \right) \times 100\%$$
*Measures how effectively the hardware cores are utilized. Ideal linear speedup yields $E = 100\%$.*

### 3. Amdahl's Law
$$S_{\max} = \frac{1}{(1 - p) + \frac{p}{P}}$$
*Where $p$ is the parallel fraction (worker chunk sorting) and $(1 - p)$ is the sequential fraction (array partitioning and reduction merge).*

> **💡 Note on IPC Overhead**: For small arrays ($N < 5{,}000$), sequential sorting is often faster because process spawning and IPC serialization take longer than the sort itself. As $N \ge 20{,}000$, parallel sorting dominates, delivering positive speedup ($S > 1.0$).

---

## 🛠️ Technology Stack

- **Frontend**:
  - React 19 + Vite
  - Lucide React (Icons & UI cues)
  - Recharts (Benchmark charts & speedup curves)
  - Pure CSS Design System (Custom properties, responsive flex/grid layouts, light/dark themes)
- **Backend**:
  - Python 3.11+
  - Flask 3.1 + Flask-CORS
  - Python Standard Library `multiprocessing` & `time.perf_counter`
  - Gunicorn (WSGI HTTP server for production)

---

## 📂 Project Structure

```text
Parallel-Sorting-Algorithm-Visualizer/
├── package.json                   # Root convenience scripts (dev, build, backend)
├── .gitignore                     # Git ignore rules for node_modules, pycache, etc.
├── README.md                      # Comprehensive project documentation
├── frontend/                      # React + Vite application
│   ├── index.html                 # App shell with SEO and metadata
│   ├── package.json               # Frontend dependencies & scripts
│   ├── vite.config.js             # Vite configuration with /api proxy
│   ├── public/                    # Static assets & SVG icons
│   └── src/
│       ├── main.jsx               # React entry point
│       ├── App.jsx                # Theme provider, tab layout & health polling
│       ├── index.css              # Dark & Light design system tokens
│       ├── algorithms/
│       │   └── sortingGenerators.js  # Generator functions for animations
│       ├── components/
│       │   ├── Navbar.jsx         # Header with tabs, core counter & theme toggle
│       │   ├── SortingPlayground.jsx  # Interactive sandbox with step controls
│       │   ├── ParallelExecution.jsx  # Multiprocessing chunk & merge tree visualizer
│       │   ├── PerformanceAnalysis.jsx# Recharts benchmark graphs & verification
│       │   ├── ArrayVisualizer.jsx# Dynamic visual element renderer
│       │   └── StatsCard.jsx      # Metrics cards
│       └── services/
│           └── api.js             # Client for Flask endpoints
└── backend/                       # Python Flask service
    ├── app.py                     # REST API endpoints & CORS configuration
    ├── algorithms.py              # Pure sequential sorting algorithms
    ├── parallel_sort.py           # Multiprocessing parallel merge sort & K-way merge
    ├── benchmark.py               # Microsecond benchmarking & 3-point verification
    ├── test_backend.py            # Unit test suite
    └── requirements.txt           # Python dependencies (flask, flask-cors, gunicorn)
```

---

## ⚙️ Installation & Local Setup

### Prerequisites
- **Node.js** (v18+) and **npm**
- **Python** (v3.10+)

### 1. Clone the Repository
```bash
git clone https://github.com/milanraj-github/Parallel-Sorting-Algorithm-Visualizer.git
cd Parallel-Sorting-Algorithm-Visualizer
```

### 2. Install Dependencies
```bash
# Frontend
npm --prefix frontend install

# Backend
pip install -r backend/requirements.txt
```

### 3. Run the Servers

#### Terminal 1 — Backend (Flask API):
```bash
python backend/app.py
```
*API will start on `http://localhost:5000`.*

#### Terminal 2 — Frontend (Vite Dev Server):
```bash
npm run dev
```
*Vite will start on `http://localhost:5173`.*

Open your browser at **`http://localhost:5173`**.

---

## 📡 Backend API Reference

| Endpoint | Method | Description | Payload Example |
| :--- | :---: | :--- | :--- |
| `/api/health` | `GET` | Health status and CPU core count | `None` |
| `/api/sort/sequential` | `POST` | Execute sequential sort algorithm | `{"array": [8, 3, 6, 1], "algorithm": "merge"}` |
| `/api/sort/parallel` | `POST` | Execute multiprocessing sort | `{"array": [8, 3, 6, 1], "num_workers": 4}` |
| `/api/benchmark` | `POST` | Live single benchmark trial | `{"size": 20000, "num_workers": 4, "trials": 1}` |
| `/api/benchmark/suite` | `POST` | Benchmark multiple sizes | `{"sizes": [1000, 5000, 20000], "num_workers": 4}` |

---

## 🧪 Automated Unit Testing

A comprehensive automated test suite covers algorithmic edge cases, chunking fairness, correctness criteria, and benchmark validity:

```bash
python backend/test_backend.py
```

Expected output:
```text
......
----------------------------------------------------------------------
Ran 6 tests in 2.2s

OK
```

---

## 🌐 Deployment Guide

### Frontend (Vercel)
1. Push repository to GitHub.
2. In Vercel, click **Add New Project** and select this repository.
3. Configure build settings:
   - **Root Directory**: `frontend`
   - **Framework Preset**: `Vite`
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`
4. Set Environment Variable:
   - `VITE_API_URL` = `https://<your-backend-url>.onrender.com`
5. Click **Deploy**.

### Backend (Render)
1. In Render, select **New Web Service**.
2. Connect your GitHub repository.
3. Set the configuration:
   - **Root Directory**: `backend`
   - **Runtime**: `Python 3`
   - **Build Command**: `pip install -r requirements.txt`
   - **Start Command**: `python app.py`
4. Click **Create Web Service**.

---

## 📜 Academic Evaluation Criteria Met

- [x] Authentic OS-level process management with `multiprocessing.Pool`
- [x] Comparative evaluation between sequential and parallel implementations
- [x] Speedup curves and parallel efficiency calculations
- [x] 3-point automated correctness verification
- [x] Responsive Light/Dark theme user interface

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
