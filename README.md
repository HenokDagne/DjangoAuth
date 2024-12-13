
# Login With User Authentication - Django

## Introduction to User Authentication

*Aimed at enabling user login directly from the website, rather than through Django's admin section.
Forms the basis for future features like registration and profile updates.
*
=======
# DjangoAuth
# Login With User Authentication - Django

## Introduction to User Authentication

* Aimed at enabling user login directly from the website, rather than through Django's admin section.
Forms the basis for future features like registration and profile updates

## Setup of a New App

* A new Django app named members is created to handle all authentication tasks (login, logout, registration, etc.).

```python
INSTALLED_APPS = [
    'login.apps.LoginConfig',
}
```

## Configuration Updates

* The new app is added to INSTALLED_APPS in settings.py.
urls.py for the new app is created.
Adjustments to the project-level urls.py to integrate Django's authentication URLs.
  
## Views and Forms

* **The login_user** view is defined to render the login page.
The view includes integration of Django's authenticate and login methods for handling user credentials.
A simple form using Bootstrap is built directly in login.html for user input.

### signuop_view

* The **signup_user view** is defined to render the signup page.
The view includes integration of Django's create_user method for handling user registration.
A simple form using Bootstrap is built directly in signup.html for user input.

#### SignUpin Code

```python

def signup_view(request):
    if request.method == 'POST':
        username = request.POST['username']
        password = request.POST['password']
        first_name = request.POST['first_name']
        last_name = request.POST['last_name']
        email = request.POST['email']

        if User.objects.filter(username=username).exists():
            messages.error(request, 'Username already exists.')
            return redirect('signup')

        user = User.objects.create_user(username=username, password=password, first_name=first_name, last_name=last_name, email=email)
        messages.success(request, 'Your account has been created successfully.')
        return redirect('login')
    return render(request, 'signup.html')

```

### Login View

The `login_view` function handles user login. It checks if the request method is POST, retrieves the username and password from the request, and authenticates the user. If the user is authenticated, they are logged in and redirected to the home page. If authentication fails, an error message is displayed.

#### LoginCode

```python
def login_view(request):
    if request.method == 'POST':
        username = request.POST['username']
        password = request.POST['password']
        user = authenticate(request, username=username, password=password)
        if user is not None:
            auth_login(request, user)
            messages.success(request, 'You have successfully logged in.')
            return redirect('home')
        else:
            messages.error(request, 'Invalid username or password.')
            return redirect('login')
    return render(request, 'login.html')

## Integration with Navigation

* A link to the login page is added to the website's navigation bar.

Replace `http://example.com/login` with the actual URL you want to link to. This will create a clickable link with the text "Login Page" that points to the specified URL.
>>>>>>> 6ef8b7d2f75d4d74b0196a092e30c95903fcbcf7
