Markdown spec
=============

Since for the moment there is no universal markdown specification,
md-toc is quite flexible during the interpretation step.

Anchor links
------------

Since anchor links are a prominent feature of md_toc so some research was 
necessary to make sure that they work under all conditions.

Markdown parsers have different behaviours regarding anchor links. Some of them 
implement them while others don't; some act on the duplicate entry problem 
while others don't; some strip consecutive dash characters while others don't; 
and so on...

Anchor types and behaviours
---------------------------

What follows is a list of parameters and rules used by md_toc to decide 
how to render anchor links.

- ``standard``: no transformation is done.

- ``github``: a translated version of the Ruby algorithm is used in md_toc. 
  The original one is repored here: 
  
  - https://github.com/jch/html-pipeline/blob/master/lib/html/pipeline/toc_filter.rb

  GitHub uses cmark-gfm:

  - https://github.com/github/cmark

  I could not dind the code directly responsable for the anchor link generation.
  See also:

  - https://github.github.com/gfm/
  - https://githubengineering.com/a-formal-spec-for-github-markdown/
  - https://github.com/github/cmark/issues/65#issuecomment-343433978

  This is the license used in md_toc:

  ::

        Copyright (c) 2012 GitHub Inc. and Jerry Cheung
        Copyright (c) 2018, Franco Masotti <franco.masotti@student.unife.it>

        MIT License

        Permission is hereby granted, free of charge, to any person obtaining
        a copy of this software and associated documentation files (the
        "Software"), to deal in the Software without restriction, including
        without limitation the rights to use, copy, modify, merge, publish,
        distribute, sublicense, and/or sell copies of the Software, and to
        permit persons to whom the Software is furnished to do so, subject to
        the following conditions:

        The above copyright notice and this permission notice shall be
        included in all copies or substantial portions of the Software.

        THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
        EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
        MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
        NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
        LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
        OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
        WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.


- ``redcarpet``: Treats consecutive dash characters by tranforming them into a 
  single dash character. A translated version of the C algorithm 
  is used in md_toc. The original version is here:

  - https://github.com/vmg/redcarpet/blob/26c80f05e774b31cd01255b0fa62e883ac185bf3/ext/redcarpet/html.c#L274

  This is the license used in md_toc:

  ::

        Copyright (c) 2009, Natacha Porté
        Copyright (c) 2015, Vicent Marti
        Copyright (c) 2018, Franco Masotti <franco.masotti@student.unife.it>

        Permission is hereby granted, free of charge, to any person obtaining a copy
        of this software and associated documentation files (the "Software"), to deal
        in the Software without restriction, including without limitation the rights
        to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
        copies of the Software, and to permit persons to whom the Software is
        furnished to do so, subject to the following conditions:
        
        The above copyright notice and this permission notice shall be included in
        all copies or substantial portions of the Software.
        THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
        IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
        FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
        AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
        LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE,  ARISING FROM,
        OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER  DEALINGS IN
        THE SOFTWARE.


  See also:

  - https://github.com/vmg/redcarpet/issues/618#issuecomment-306476184
  - https://github.com/vmg/redcarpet/issues/307#issuecomment-261793668

- ``gitlab``: GitLab uses the Redcarpet parser with some modifications, such 
  as duplicate anchor link detection. A generic pseudocode is
  available here:

  - https://gitlab.com/help/user/markdown.md#header-ids-and-links
              
- ``gogs``, ``marked``, ``notabug``: Gogs uses marked as the markdown 
  parser while *NotABug.org is powered by a liberated version of gogs*. 
  Situation seems unclear. Here are some links:

  - https://gogs.io/docs
  - https://github.com/chjj/marked
  - https://github.com/chjj/marked/issues/981
  - https://github.com/chjj/marked/search?q=anchor&type=Issues&utf8=%E2%9C%93
  - https://notabug.org/hp/gogs/

  For this reason no implementation is available for the moment.

- ``kramdown``: It is unclear if this feature is available. See:

  - https://github.com/gettalong/kramdown/search?q=anchor&type=Issues&utf8=%E2%9C%93
