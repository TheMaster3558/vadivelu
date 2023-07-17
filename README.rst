Vadivelu
========
A Python library for accessing the `Vadivelu API <https://vadivelu.anoram.com/>`_.

Installation
------------
**Must have Python 3.5 or higher**

.. code:: sh

    pip install vadivelu

API Reference
-------------

.. code:: python

    .. py:function:: get_available_formats(code)
      :module: vadivelu
      :param code: The HTTP code to use
      :type code: :class:`int`

      Get the available formats for a HTTP code. The formats can be gif, jpg, or both.

      :rtype: :class:`Tuple[str, str]`
      :returns:  A tuple containing the available formats
      :raises: :class:`ValueError` if the code is not a code supported by the API

    .. py:function:: pick_available_format(code, priority)
      :module: vadivelu
      :param code: The HTTP code to use
      :type code: :class:`int`
      :param priority: The format to pick in the case both gif and jpg are available (default: gif)
      :type priority: :class:`str`

      Pick a format (gif or jpg) that the API supports for a specific HTTP code.

      :rtype: :class:`str`
      :returns: The picked format (gif or jpg)
      :raises: :class:`ValueError` ``priority`` is not gif or jpg

    .. py:function:: get_media_url(code, media_format)
      :module: vadivelu
      :param code: The HTTP code to use
      :type code: :class:`int`
      :param media_format: The media format to get (gif or jpg)
      :type media_format: :class:`str`

      Get the media URL for the specified code in the specified format.

      :rtype: :class:`str`
      :returns: The URL for the media
      :raises: :class:`ValueError` ``media_format`` is not available for the given code, use :func:`pick_available_format` to avoid this error

Example
-------

.. code:: python

    import requests
    import vadivelu

    code = 404
    url = vadivelu.get_media_url(code, vadivelu.pick_available_format(code, 'jpg'))

    # save jpg to 404.jpg file
    with open('404.jpg', 'wb') as f:
        f.write(requests.get(url).content)
