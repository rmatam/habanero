habanero
========

|pypi| |docs| |travis| |coverage|

This is a low level client for working with Crossref's search API. It's been named to be more generic, as other organizations are/will adopt Crossref's search API, making it possible to interact with all from one client.

`Crossref API docs <https://github.com/CrossRef/rest-api-doc/blob/master/rest_api.md>`__

Other Crossref API clients:

- Ruby: `serrano`, `<https://github.com/sckott/serrano>`__
- R: `rcrossref`, `<https://github.com/ropensci/rcrossref>`__

`habanero` includes three modules you can import as needed (or
import all):

`Crossref` - Crossref search API. The `Crossref` module includes methods matching Crossref API routes, and a few convenience methods for getting DOI agency and random DOIs:

- `works` - `/works` route
- `members` - `/members` route
- `prefixes` - `/prefixes` route
- `funders` - `/funders` route
- `journals` - `/journals` route
- `types` - `/types` route
- `licenses` - `/licenses` route
- `registration_agency` - get DOI minting agency
- `random_dois` - get random set of DOIs

`counts` - citation counts. Includes the single `citation_count` method

`cn` - content negotiation. Includes the methods:

- `content_negotiation` - get citations in a variety of formats
- `csl_styles` - get CSL styles, used in `content_negotation` method

Note about searching:

You are using the Crossref search API described at https://github.com/CrossRef/rest-api-doc/blob/master/rest_api.md. When you search with query terms, on Crossref servers they are not searching full text, or even abstracts of articles, but only what is available in the data that is returned to you. That is, they search article titles, authors, etc. For some discussion on this, see https://github.com/CrossRef/rest-api-doc/issues/101


Installation
============

Stable version

.. code-block:: console

  pip install habanero

Dev version

.. code-block:: console

    sudo pip install git+git://github.com/sckott/habanero.git#egg=habanero

    # OR

    git clone git@github.com:sckott/habanero.git
    cd habanero
    make install

Usage
=====

Initialize a client

.. code-block:: python

    from habanero import Crossref
    cr = Crossref()

Works route

.. code-block:: python

  x = cr.works(query = "ecology")
  x['message']
  x['message']['total-results']
  x['message']['items']

Members route

.. code-block:: python

  cr.members(ids = 98, works = True)

Citation counts

.. code-block:: python

  from habanero import counts
  counts.citation_count(doi = "10.1016/j.fbr.2012.01.001")

Content negotiation - get citations in many formats

.. code-block:: python

  from habanero import cn
  cn.content_negotiation(ids = '10.1126/science.169.3946.635')
  cn.content_negotiation(ids = '10.1126/science.169.3946.635', format = "citeproc-json")
  cn.content_negotiation(ids = "10.1126/science.169.3946.635", format = "rdf-xml")
  cn.content_negotiation(ids = "10.1126/science.169.3946.635", format = "text")
  cn.content_negotiation(ids = "10.1126/science.169.3946.635", format = "text", style = "apa")
  cn.content_negotiation(ids = "10.1126/science.169.3946.635", format = "bibentry")

Meta
====

* Please note that this project is released with a `Contributor Code of Conduct <https://github.com/sckott/habanero/blob/master/CONDUCT.md>`__. By participating in this project you agree to abide by its terms.
* License: MIT; see `LICENSE file <https://github.com/sckott/habanero/blob/master/LICENSE>`__

.. |pypi| image:: https://img.shields.io/pypi/v/habanero.svg
   :target: https://pypi.python.org/pypi/habanero

.. |docs| image:: https://readthedocs.org/projects/habanero/badge/?version=latest
   :target: http://habanero.rtfd.org/

.. |travis| image:: https://travis-ci.org/sckott/habanero.svg?branch=master
   :target: https://travis-ci.org/sckott/habanero

.. |coverage| image:: https://coveralls.io/repos/sckott/habanero/badge.svg?branch=master&service=github
   :target: https://coveralls.io/github/sckott/habanero?branch=master

