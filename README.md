<h1 align="center">github-hosted-pypi</h1>

<p align="center">
Make all your private packages accessible in one place<br>with this github-hosted PyPi index
</p>

---

<p align="center">
  <a href="#description">Description</a> •
  <a href="#try-it-">Try it !</a> •
  <a href="#get-started">Get Started</a> •
  <a href="#modify-indexed-packages">Modify indexed packages</a> •
  <a href="#faq">FAQ</a> •
  <a href="#contribute">Contribute</a> •
  <a href="#references">References</a>
</p>

---

## Features

* **:octocat: Github-hosted**
* **🚀 Template ready to deploy**
* **🔆 Easy to use** through Github Actions

## Description

This repository is a Github page used as a PyPi index, conform to [PEP503](https://www.python.org/dev/peps/pep-0503/).

You can use it to group all your packages in one place, and access it easily through `pip`, almost like any other package publicly available !

---

_While the PyPi index is public, private packages indexed here are kept private : you will need Github authentication to be able to retrieve it._

## Try it !

Visit [astariul.github.io/github-hosted-pypi/](http://astariul.github.io/github-hosted-pypi/) and try to install packages indexed there !

---

Try to install the package `public-hello` :
```console
pip install public-hello --extra-index-url https://astariul.github.io/github-hosted-pypi/
```

It will also install the package `mydependency`, automatically ! 

Try it with :

```python
from public_hello import hi
print(hi())
```

You can also install a specific version :

```console
pip install public-hello==0.1 --extra-index-url https://astariul.github.io/github-hosted-pypi/
```

---

Now try to install the package `private-hello` :
```console
pip install private-hello --extra-index-url https://astariul.github.io/github-hosted-pypi/
```

_It will not work, because it's private and only me can access it !_

## Get started

* Use this template and create your own repository : [![Generic badge](https://img.shields.io/badge/Use%20this%20template-blueviolet.svg)](https://github.com/astariul/github-hosted-pypi/generate)
* Go to `Settings` of your repository, and enable Github Page
* Customize `index.html` and `pkg_template.html` to your liking
* You're ready to go ! Visit `<user>.github.io/<repo_name>` to see your PyPi index

## Modify indexed packages

Now that your PyPi index is setup, you can register / update / delete packages indexed.  
_Github actions are setup to do it automatically for you._

You just have to :
* Open an issue with the appropriate template
* Fill the information of the template (replace the comments)
* Wait a bit
* Check the new PR opened (ensure the code added correspond to what you want)
* Merge the PR

## FAQ

#### Q. Is it secure ?

As you may know, `pip` can install Github-hosted package if given in the form `pip install git+<repo_link>`. This PyPi index is just an index of links to other Github repository.

Github pages are public, so this PyPi index is public. But it just contain links to other Github repositories, no code is hosted on this PyPi index !.  

If the repository hosting code is private, you will need to authenticate with Github to be able to clone it, effectively making it private.

#### Q. What happen behind the scenes ?

When running `pip install <package_name> --extra-index-url https://astariul.github.io/github-hosted-pypi/`, the following happen :

1. `pip` will look at `https://pypi.org/`, the default, public index, trying to find a package with the specified name.
2. If it can't find, it will look at `https://astariul.github.io/github-hosted-pypi/`.
3. If the package is found there, the link of the package is returned to `pip` (`git+<repo_link>@<tag>`).
4. From this link, `pip` understand it's a Github repository and will clone the repository (at the specific tag) locally.
5. From the cloned repository, `pip` install the package.
6. `pip` install any missing dependency with the same steps.

_Authentication happen at step 4, when cloning the repository._

#### Q. What are the best practices for using this PyPi index ?

The single best practice is using Github releases. This allow your package to have a version referred by a specific tag.  
To do this :

* Push your code in a repository.
* Create a new Github release. Ensure you follow [semantic versioning](https://semver.org/). It will create a tag.
* Ensure you can install the package with `pip install git+<repo_link>@<tag>`
* When putting the package on this index, put the full link (`git+<repo_link>@<tag>`).

#### Q. What if the name of my package is already taken by a package in the public index ?

You can just specify a different name for your indexed package. Just give it a different name in the form when registering it.

For example if you have a private package named `tensorflow`, when you register it in this index, you can name it `my_cool_tensorflow`, so there is no name-collision with the public package `tensorflow`.  
Then you can install it with `pip install my_cool_tensorflow --extra-index-url https://astariul.github.io/github-hosted-pypi/`.

Then from `python`, you can just do :
```python
import tensorflow
```

_Note : While it's possible to do like this, it's better to have a unique name for your package, to avoid confusion._

## Contribute

Issues and PR are welcome !

If you come across anything weird / that can be improved, please get in touch !

## References

**This is greatly inspired from [this repository](https://github.com/ceddlyburge/python-package-server).**  
It's just a glorified version, with cleaner pages and github actions for easily adding, updating and removing packages from your index.

Also check the [blogpost](https://www.freecodecamp.org/news/how-to-use-github-as-a-pypi-server-1c3b0d07db2/) of the original author !

---

_Icon used in the page was made by [Freepik](https://www.flaticon.com/authors/freepik) from [Flaticon](https://www.flaticon.com/)_
