# MOKSMART — Complete E-Commerce System

Django + SQLite classroom project with customer shopping and staff administration.

## Included modules
### Customer
- Register, login, logout
- Browse/search/filter active products and view product details
- Session-based shopping cart (add, update quantity, remove)
- Checkout with shipping details and Cash on Delivery / Bank Transfer selection
- Order confirmation, order history, order detail
- Edit basic account profile

### Administrator (Django staff account)
- Admin dashboard with product/customer/order metrics
- Product CRUD (create/read/update/delete)
- Customer list and account deactivation (preserves order history)
- Order list and status update (pending, processing, shipped, delivered, cancelled)
- Cancelling an order restores stock
- Django Admin at `/django-admin/`

## Setup on Windows / VS Code
1. Extract this ZIP and open `MOKSMART_FULL` in VS Code.
2. In the terminal:
   ```bash
   python -m venv venv
   venv\Scripts\activate
   pip install -r requirements.txt
   python manage.py makemigrations store
   python manage.py migrate
   python manage.py createsuperuser
   python manage.py runserver
   ```
3. Visit `http://127.0.0.1:8000/` for the customer storefront.
4. Visit `http://127.0.0.1:8000/login/` and log in with the superuser credentials. Staff users are redirected to the admin dashboard.
5. Admin dashboard: `http://127.0.0.1:8000/manage/`
6. Django admin: `http://127.0.0.1:8000/django-admin/`

## Add products
Log in as staff, open Manage Products, and add products. Set status to Active and stock above zero for customers to see them.

## Important implementation notes
- Cart is session-based; customer must log in to add items and checkout.
- Checkout validates stock and creates an order plus order-item snapshots. Stock is deducted at order placement.
- Payment options are recorded selections only. No live payment gateway or bank verification is integrated.
- Shipping fees are not calculated. No courier API, email/SMS notifications, or customer reviews are included.
- Customer deactivation is used instead of deleting a user because existing orders reference that customer.
- Before deployment: set a strong SECRET_KEY, DEBUG=False, production ALLOWED_HOSTS, HTTPS, secure cookies, and a production database. Add real payment integration only through a trusted provider.
