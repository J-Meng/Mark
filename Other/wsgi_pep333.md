WSGI is an interface specification by which server and application communicate. Both server and application interface interface sides are specified.

It exist in the PEP3333.

Please see detail of PEP3333:
'''
http://legacy.python.org/dev/peps/pep-3333/
'''

We use the middle-ware to verify the Authorization

'''
#At wsgi.py 
import AuthMiddleware

class Application(Flask):
    def __init__(self, *args, **kwargs):
        ...
        self.wsgi_app = Middleware(self.wsgi_app, self.validate_with_swp)
        ...
'''
#AuthMiddleware

class Middleware:
    def __init__(self, app, swp_validator):
        self.app = app
        self.validator = swp_validator
    def __call__(self, environ, start_response):
        ...
        def _start_res(status, headers):
            #validator ok
            #create respinse_headers

            return start_response(status, response_headers)
        ...
        # So we can do validate here:
        authorization = environ.pop("HTTP_authorization")

        return self.app(environ, _start_res)
'''

check the environ Variables
