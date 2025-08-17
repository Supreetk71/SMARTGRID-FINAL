# Smart Grid Management System

Autonomous Smart Grid Management Agent that integrates with Central Electricity Authority API to monitor, forecast, and optimize electrical grid operations.

## Overview

The Smart Grid Management System is a comprehensive solution for monitoring and managing power grids. It provides:

- Real-time monitoring of power generation and consumption
- Demand forecasting using machine learning
- Load balancing optimization
- Fault detection and analysis
- Renewable energy source monitoring

## Features

- **Dashboard**: View current grid status, power generation/consumption, and regional distribution
- **Forecasting**: Predict future power demand using machine learning
- **Load Balancing**: Simulate different load balancing scenarios across regions
- **Fault Detection**: Identify and analyze potential issues in the grid
- **Renewable Sources**: Monitor renewable energy generation and capacity

## Installation

### Prerequisites

- Python 3.10 or higher
- PostgreSQL database

### Standard Installation

1. **Clone the repository**

```bash
git clone https://github.com/yourusername/smart-grid-management.git
cd smart-grid-management
```

2. **Virtual environment**

```bash
python -m venv venv
```

3. **Activate the virtual environment**

On Windows:
```bash
venv\Scripts\activate
```

On macOS/Linux:
```bash
source venv/bin/activate
```

4. **Install dependencies**

```bash
pip install flask flask-sqlalchemy gunicorn Werkzeug
pip install psycopg2-binary SQLAlchemy
pip install numpy pandas matplotlib scikit-learn
pip install requests
pip install email-validator
```

Or create a requirements.txt file with the following content and run `pip install -r requirements.txt`:

```
flask==2.3.3
flask-sqlalchemy==3.1.1
gunicorn==23.0.0
Werkzeug==2.3.7
psycopg2-binary==2.9.9
SQLAlchemy==2.0.23
numpy==2.2.5
pandas==2.2.3
matplotlib==3.10.1
scikit-learn==1.6.1
requests==2.32.3
email-validator==2.1.0
```

5. **Set up database**

Ensure PostgreSQL is running, then set the following environment variables:

```bash
# Windows
set DATABASE_URL=postgresql://username:password@localhost:5432/smartgrid

# macOS/Linux
export DATABASE_URL=postgresql://username:password@localhost:5432/smartgrid
```

6. **Run the application**

```bash
python main.py
```

The application will be available at `http://localhost:5000`.

## Running as a Windows 11 App

Package this application as a Windows 11 app using PyInstaller and create a desktop shortcut.

### Packaging with PyInstaller

1. **Install PyInstaller**

```bash
pip install pyinstaller
```

2. **Create spec file**

Create a file named `smart_grid.spec` with the following content:

```
# -*- mode: python ; coding: utf-8 -*-

block_cipher = None

a = Analysis(
    ['main.py'],
    pathex=[],
    binaries=[],
    datas=[
        ('templates', 'templates'),
        ('static', 'static'),
    ],
    hiddenimports=['sklearn.ensemble', 'sklearn.preprocessing', 'sklearn.model_selection'],
    hookspath=[],
    hooksconfig={},
    runtime_hooks=[],
    excludes=[],
    win_no_prefer_redirects=False,
    win_private_assemblies=False,
    cipher=block_cipher,
    noarchive=False,
)
pyz = PYZ(a.pure, a.zipped_data, cipher=block_cipher)

exe = EXE(
    pyz,
    a.scripts,
    [],
    exclude_binaries=True,
    name='SmartGridManagement',
    debug=False,
    bootloader_ignore_signals=False,
    strip=False,
    upx=True,
    console=False,
    disable_windowed_traceback=False,
    argv_emulation=False,
    target_arch=None,
    codesign_identity=None,
    entitlements_file=None,
    icon='static/img/favicon.ico',
)
coll = COLLECT(
    exe,
    a.binaries,
    a.zipfiles,
    a.datas,
    strip=False,
    upx=True,
    upx_exclude=[],
    name='SmartGridManagement',
)
```

3. **Create a batch file to set up the environment**

Create a file named `start_smart_grid.bat` with the following content:

```batch
@echo off
SET DATABASE_URL=postgresql://username:password@localhost:5432/smartgrid
start "" "dist\SmartGridManagement\SmartGridManagement.exe"
```

4. **Build the executable**

```bash
pyinstaller smart_grid.spec
```

5. **Create Desktop Shortcut**

- Right-click desktop
- Select "New > Shortcut"
- Browse to the location of `start_smart_grid.bat`
- Name the shortcut "Smart Grid Management"
- Right-click the shortcut and select "Properties"
- Click "Change Icon" and select an icon (you can use one from the static folder)
- Click "OK" to save the changes

6. **Run the application**

Double-click the desktop shortcut to run the application.

## API Documentation

The application provides the following API endpoints:

- `/api/grid-data`: Get current grid status and power data
- `/api/renewable-data`: Get renewable energy generation data
- `/api/forecast-demand`: Generate power demand forecast
- `/api/simulate-balancing`: Simulate load balancing scenarios
- `/api/detect-faults`: Identify potential faults in the grid

## Configuration

The application can be configured using environment variables:

- `DATABASE_URL`: PostgreSQL connection URL
- `CEA_API_KEY`: API key for Central Electricity Authority (optional)
- `SESSION_SECRET`: Secret key for Flask sessions

## About Simulated Data

Application is designed to work with the Central Electricity Authority (CEA) API, but it also includes a robust fallback mechanism that generates simulated data when the actual API is not available. This allows for:

1. Development and testing without requiring API access
2. Demonstration of all features using realistic simulated grid data
3. Graceful handling of API outages or connectivity issues

The simulated data includes:
- Power generation and consumption data for different regions
- Renewable energy capacity and generation statistics
- Historical data for demand forecasting
- Grid status including potential fault scenarios

To use real data from the CEA API (when available), you'll need to obtain an API key and set it as the `CEA_API_KEY` environment variable. When a valid API key is not provided, the system automatically uses simulated data.

## Database Schema

The application uses the following database models:

- `GridData`: Stores grid power data
- `RenewableData`: Stores renewable energy data
- `ForecastData`: Stores demand forecasts
- `PowerOutage`: Stores power outage information
- `LoadBalancingEvent`: Stores load balancing events

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### App Images:
- ![Screenshot 2025-04-30 131522](https://github.com/user-attachments/assets/2eab4055-4308-495b-a8f4-abe870e0538d)
- ![Screenshot 2025-04-30 131744](https://github.com/user-attachments/assets/5a3a6471-505f-44d8-abca-517e30e82306)

## Developer Guide

### Project Structure

```
SmartGridMaster-feature-amazing-feature/
├── app.py                 # Main Flask application
├── models.py             # Database models and schemas
├── api_client.py         # CEA API integration and data fetching
├── forecasting.py        # Machine learning forecasting algorithms
├── utils.py              # Utility functions and helpers
├── main.py               # Application entry point
├── templates/            # HTML templates
├── static/               # CSS, JS, and static assets
├── venv/                 # Virtual environment
└── pyproject.toml        # Project dependencies and configuration
```

### Development Setup

1. **Clone and setup**
```bash
git clone <repository-url>
cd SmartGridMaster-feature-amazing-feature
python -m venv venv
venv\Scripts\activate  # Windows
# source venv/bin/activate  # macOS/Linux
```

2. **Install development dependencies**
```bash
pip install -r requirements.txt
pip install pytest pytest-cov black flake8 mypy
```

3. **Code formatting and linting**
```bash
# Format code with Black
black .

# Lint with flake8
flake8 .

# Type checking with mypy
mypy .
```

### Architecture Overview

The application follows a modular architecture:

- **Flask App (`app.py`)**: Main application with routes and views
- **Data Layer (`models.py`)**: SQLAlchemy models for database operations
- **API Integration (`api_client.py`)**: External API communication and data fetching
- **ML Engine (`forecasting.py`)**: Machine learning algorithms for demand prediction
- **Utilities (`utils.py`)**: Helper functions and common operations

### Key Components

#### 1. Grid Data Management
- Real-time power grid monitoring
- Historical data storage and retrieval
- Regional power distribution tracking

#### 2. Forecasting Engine
- Time series analysis using scikit-learn
- Multiple forecasting models (Linear Regression, Random Forest)
- Demand prediction for different time horizons

#### 3. Load Balancing Simulation
- Grid load distribution algorithms
- Regional power transfer simulation
- Optimization scenarios for grid stability

#### 4. Fault Detection System
- Anomaly detection in power data
- Predictive maintenance indicators
- Grid health monitoring

### Database Models

```python
# Key models in models.py
class GridData(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    timestamp = db.Column(db.DateTime, nullable=False)
    region = db.Column(db.String(100), nullable=False)
    generation = db.Column(db.Float, nullable=False)
    consumption = db.Column(db.Float, nullable=False)
    surplus = db.Column(db.Float, nullable=False)

class RenewableData(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    source_type = db.Column(db.String(50), nullable=False)
    capacity = db.Column(db.Float, nullable=False)
    generation = db.Column(db.Float, nullable=False)
    efficiency = db.Column(db.Float, nullable=False)
```

### API Endpoints

| Endpoint | Method | Description | Parameters |
|----------|--------|-------------|------------|
| `/api/grid-data` | GET | Current grid status | `region` (optional) |
| `/api/renewable-data` | GET | Renewable energy data | `source_type` (optional) |
| `/api/forecast-demand` | POST | Generate demand forecast | `days`, `region` |
| `/api/simulate-balancing` | POST | Load balancing simulation | `scenario`, `regions` |
| `/api/detect-faults` | GET | Fault detection analysis | `severity` (optional) |

### Testing

```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=.

# Run specific test file
pytest test_forecasting.py

# Run tests with verbose output
pytest -v
```

### Environment Variables

```bash
# Required
DATABASE_URL=postgresql://username:password@localhost:5432/smartgrid

# Optional
CEA_API_KEY=your_api_key_here
SESSION_SECRET=your_secret_key_here
FLASK_ENV=development
DEBUG=True
```

### Deployment

#### Local Development
```bash
python main.py
# or
flask run --debug
```

#### Production
```bash
# Using Gunicorn
gunicorn -w 4 -b 0.0.0.0:5000 app:app

# Using Waitress (Windows)
waitress-serve --host=0.0.0.0 --port=5000 app:app
```

### Troubleshooting

#### Common Issues

1. **Database Connection Error**
   - Verify PostgreSQL is running
   - Check DATABASE_URL environment variable
   - Ensure database exists and user has permissions

2. **Import Errors**
   - Activate virtual environment
   - Install missing dependencies: `pip install -r requirements.txt`

3. **API Errors**
   - Check CEA_API_KEY if using real API
   - Verify network connectivity
   - System will fallback to simulated data

#### Debug Mode

Enable debug mode for development:
```python
# In app.py
app.config['DEBUG'] = True
```

### Performance Optimization

- Database indexing on frequently queried fields
- Caching for API responses
- Efficient data aggregation queries
- Background task processing for heavy computations

### Security Considerations

- Input validation on all API endpoints
- SQL injection prevention with SQLAlchemy ORM
- Environment variable management for sensitive data
- Rate limiting for API endpoints

## License

Distributed under the MIT License. See `LICENSE` for more information.

## Contact

   Name - email@example.com

Project Link: [https://github.com/username/smart-grid-management](https://github.com/username/smart-grid-management)
