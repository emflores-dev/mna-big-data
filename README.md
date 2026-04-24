# mna-big-data

PySpark / Spark learning environment running on Docker. Includes JupyterLab for notebooks and a shared volume for scripts and data.

## Requirements

- [OrbStack](https://orbstack.dev/) or [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [Git](https://git-scm.com/)
- [GitHub CLI](https://cli.github.com/) (optional)

## Setup

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/mna-big-data.git
cd mna-big-data
```

### 2. Create the local folders

```bash
mkdir notebooks scripts data
```

### 3. Start the environment

```bash
docker compose up
```

> The first run will pull the image (~2GB), so it may take a few minutes.

### 4. Open JupyterLab

Look for a URL in the terminal output like:
http://127.0.0.1:8888/lab?token=<your-token>

Open it in your browser.

### 5. Spark UI (optional)

While a PySpark session is active, visit:
http://localhost:4040

## Project structure

```text
mna-big-data/
├── docker-compose.yml   # Environment definition
├── notebooks/           # Jupyter notebooks (.ipynb)
├── scripts/             # PySpark scripts (.py)
└── data/                # Input/output data files
```

## Running a script

With the container running, open a new terminal and run:

```bash
docker exec pyspark-learn spark-submit /home/jovyan/scripts/your_script.py
```

## Starting a PySpark session in a notebook

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("my-app") \
    .master("local[*]") \
    .getOrCreate()
```

## Stop the environment

```bash
docker compose down
```

## Notes

- All files in `notebooks/`, `scripts/`, and `data/` are mounted from your local machine — they persist across restarts.
- `local[*]` uses all available CPU cores on your machine.
- The Spark UI at port 4040 is only active while a SparkSession is running.
