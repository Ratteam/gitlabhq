# Syntax Highlighting

GitLab provides syntax highlighting on all files through the [Rouge](https://rubygems.org/gems/rouge) Ruby gem. It will try to guess what language to use based on the file extension, which most of the time is sufficient.

NOTE: **Note:**
The [Web IDE](web_ide/index.md) and [Snippets](../snippets.md) use [Monaco Editor](https://microsoft.github.io/monaco-editor/)
for text editing, which internally uses the [Monarch](https://microsoft.github.io/monaco-editor/monarch.html)
library for syntax highlighting.

If GitLab is guessing wrong, you can override its choice of language using the `gitlab-language` attribute in `.gitattributes`. For example, if you are working in a Prolog project and using the `.pl` file extension (which would normally be highlighted as Perl), you can add the following to your `.gitattributes` file:

``` conf
*.pl gitlab-language=prolog
```

When you check in and push that change, all `*.pl` files in your project will be highlighted as Prolog.

The paths here are simply Git's built-in [`.gitattributes` interface](https://git-scm.com/docs/gitattributes). So, if you were to invent a file format called a `Nicefile` at the root of your project that used Ruby syntax, all you need is:

``` conf
/Nicefile gitlab-language=ruby
```

To disable highlighting entirely, use `gitlab-language=text`. Lots more fun shenanigans are available through CGI options, such as:

``` conf
# json with erb in it
/my-cool-file gitlab-language=erb?parent=json

# an entire file of highlighting errors!
/other-file gitlab-language=text?token=Error
```

Please note that these configurations will only take effect when the `.gitattributes` file is in your default branch (usually `master`).

NOTE: **Note:**
The Web IDE does not support `.gitattribute` files, but it's [planned for a future release](https://gitlab.com/gitlab-org/gitlab/-/issues/22014).
