- this statis site is built using Jekyll (using Ruby programming language)
- use `bundle exec jekyll serve --livereload` to serve
- use `bundle install` to update ruby dependencies (`gem`)
- uses Google domain www.oscarli.one (under oscarliduke account)
- edited multiple scss styling details based on minimal mistakes
    for example,
    - remove hyperlink underscore
    - increase author avatar size
    - allow line break in author bio
- mathjax
    - to use mathjax, we follow the instructions given in 
    `https://docs.mathjax.org/en/latest/web/configuration.html`
    by pasting the `<script></script>` into `_layouts/default.html`.
    - This allows using single dollar `$` sign for inline math and `\\[` `\\]` for
    block equation.
- `_code/` for storing code artefacts.