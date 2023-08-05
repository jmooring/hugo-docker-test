+++
title = 'reStructuredText'
date = 2021-10-22T19:01:00-07:00
draft = false
+++

The build will fail under either of the following conditions:

- Rst2html is not installed
- The `security.exec.allow` list does not include `rst2html.py`

This is an equation in reStructuredText markdown:

  ``:math:`A_\text{c} = \pi r^2```

This is how it renders:

  :math:`A_\text{c} = \pi r^2`
