# Django Standards

## Framework
- Use Django REST Framework (DRF) for all API projects
- Python 3.11+ required
- Use `django-environ` for environment variable management

## Models
- Define all fields explicitly — avoid implicit defaults
- Add field-level validators where applicable
- Extend `AbstractUser` from day one — never use default `User` model
- Use `Meta.ordering`, `__str__`, and `verbose_name` on all models
- One migration per logical change — keep migrations focused

## Views & Serializers
- Use `ModelViewSet` for standard CRUD operations
- Use separate serializers for read (list/retrieve) and write (create/update)
- Keep business logic in service functions or model methods — not in views
- Use `select_related` and `prefetch_related` to avoid N+1 queries

## Settings
- Split settings: `base.py`, `dev.py`, `staging.py`, `prod.py`
- `base.py` contains shared config, environment-specific files import from base
- Never hardcode secrets — use `django-environ` to read from `.env`
- `DEBUG = False` in production — enforced, never overridden

## URL Patterns
- Use DRF routers for viewset URL registration
- API URLs namespaced: `/api/v1/`
- Use `path()` not `re_path()` unless regex is truly needed

## Project Structure
```
project/
├── config/               # Settings, URLs, WSGI/ASGI
│   ├── settings/
│   │   ├── base.py
│   │   ├── dev.py
│   │   └── prod.py
│   ├── urls.py
│   └── wsgi.py
├── apps/
│   └── users/
│       ├── models.py
│       ├── serializers.py
│       ├── views.py
│       ├── services.py
│       ├── urls.py
│       └── tests/
├── common/               # Shared utilities
└── manage.py
```
