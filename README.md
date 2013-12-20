_python
=======

import urllib,json
from urllib.request import urlopen
from wsgiref.simple_server import make_server
from pyramid.config import Configurator
from pyramid.response import Response
from pyramid.request import Request


def fetch_data(request):
    url="http://xola.com/api/experiences"
    data = json.loads((urllib.request.urlopen(url)).read().decode("utf-8"))    
    return Response(data)

if __name__ == '__main__':
    config = Configurator()
    config.add_route('adr', '/fetch')
    config.add_view(fetch_data, route_name='adr')
    app = config.make_wsgi_app()
    server = make_server('0.0.0.0', 8080, app)
    server.serve_forever()
