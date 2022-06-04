## set up
1. set up environment
    - install python >3.6
    - install virtual env: 
    python3 -m venv venv
    . venv/bin/activate
2. set Flask and Flask-SQLAchemy to work with database
    - pip install Flask Flask-SQLAlchemy


## Initiate 
add app.py
add templates/base.html


## run & test
export FLASK_APP=app.py
export FLASK_ENV=development
flask run