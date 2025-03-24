# <img src="https://fonts.gstatic.com/s/e/notoemoji/latest/1f680/512.gif" alt="🚀" width="32" height="32"> Deploying a Django Project on Render

Welcome to the **Django Deployment Guide on Render**! 🎉 This repository provides a step-by-step guide to deploying a Django project on **Render**, including necessary Git commands.

## <img src="https://fonts.gstatic.com/s/e/notoemoji/latest/270f_fe0f/512.gif" alt="✏️" width="32" height="32"> Prerequisites
Before you begin, ensure you have:
- A **Django project** ready for deployment
- A **Render account** ([Sign up here](https://render.com))
- **Git installed** on your system
- A **PostgreSQL database** (optional but recommended)

---

## <img src="https://fonts.gstatic.com/s/e/notoemoji/latest/1f4a1/512.gif" alt="💡" width="32" height="32"> Step 1: Set Up a Git Repository
1. Initialize a Git repository in your Django project:
   ```sh
   git init
   ```
2. Add all project files:
   ```sh
   git add .
   ```
3. Commit the changes:
   ```sh
   git commit -m "Initial commit"
   ```
4. Create a new repository on GitHub and add the remote origin:
   ```sh
   git remote add origin https://github.com/your-username/your-repo.git
   ```
5. Push the project to GitHub:
   ```sh
   git push -u origin main
   ```

---

## <img src="https://fonts.gstatic.com/s/e/notoemoji/latest/1f4a1/512.gif" alt="💡" width="32" height="32"> Step 2: Prepare the Django Project for Deployment
1. Install **Gunicorn** and **Whitenoise** for handling static files:
   ```sh
   pip install gunicorn whitenoise
   ```
2. Update `settings.py`:
   ```python
   import os

   ALLOWED_HOSTS = ['your-render-url.onrender.com'] # or allow all host --> '*'

   TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR, 'templates')],
         ...
   }]
   
   MIDDLEWARE = [
       'django.middleware.security.SecurityMiddleware',
       'whitenoise.middleware.WhiteNoiseMiddleware',  # Add this line
       ...
   ]

   STATICFILES_STORAGE = "whitenoise.storage.CompressedManifestStaticFilesStorage"

   STATIC_URL = '/static/'
   MEDIA_URL = '/media/'

   STATIC_ROOT = os.path.join(BASE_DIR,'staticfiles')
   MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
   ```

3. Create a `requirements.txt` file:
   ```sh
   pip freeze > requirements.txt
   # or add packages manually in this file.
   ```
4. Create a `runtime.txt` file to specify the Python version:
   ```sh
   echo "python-3.9" > runtime.txt
   ```
5. Add a `Procfile` to specify how Render should run your app:
   ```sh
   echo "web: gunicorn your_project.wsgi" > Procfile
   ```
6. Migrate the database and collect static files:
   ```sh
   python manage.py migrate
   python manage.py collectstatic --noinput
   ```
7. Commit the changes:
   ```sh
   git add .
   git commit -m "Prepare for deployment"
   git push origin main
   ```

---

## <img src="https://fonts.gstatic.com/s/e/notoemoji/latest/1f4a1/512.gif" alt="💡" width="32" height="32"> Step 3: Deploy to Render
1. Go to [Render](https://dashboard.render.com/) and create a new **Web Service**.
2. Connect your **GitHub repository**.
3. Set the **Build Command**:
   ```sh
   pip install -r requirements.txt && python manage.py migrate && python manage.py collectstatic --noinput
   ```
4. Set the **Start Command**:
   ```sh
   gunicorn your_project.wsgi
   ```
5. Choose **Free or Paid Plan** and click **Deploy**.

---


## <img src="https://fonts.gstatic.com/s/e/notoemoji/latest/1f4a1/512.gif" alt="💡" width="32" height="32"> Step 5: Final Steps
- Visit your **Render deployment URL**.
- If you face issues, check logs using:
  ```sh
  render logs
  ```
- <img src="https://fonts.gstatic.com/s/e/notoemoji/latest/1f386/512.gif" alt="🎆" width="32" height="32"> Congratulations! Your Django app is live! <img src="https://fonts.gstatic.com/s/e/notoemoji/latest/1f680/512.gif" alt="🚀" width="32" height="32">

---

<br>
<br>
Let me know if you need any clarifications or additional steps! <img src="https://fonts.gstatic.com/s/e/notoemoji/latest/1f31f/512.gif" alt="🌟" width="32" height="32">


## <img src="https://fonts.gstatic.com/s/e/notoemoji/latest/2764_fe0f/512.gif" alt="❤" width="32" height="32"> Show Some Love!  
If you liked this, consider giving it a ⭐ and following me! 🚀  

[![GitHub followers](https://img.shields.io/github/followers/aman-khan001?label=Follow%20Me&style=social)](https://github.com/aman-khan001)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=flat&logo=linkedin)](https://www.linkedin.com/in/aman-khan001/)  

   <img src="https://media.giphy.com/media/3o7abKhOpu0NwenH3O/giphy.gif" width="200px">


<br>
<br>
