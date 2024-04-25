---
layout: post
title:  "Upload package to PyPI"
date:   2024-04-17
categories: Learning-notes
comments: true
---

> Introduction to how to upload your own package project to PyPI.

> PyPI site: [link](https://packaging.python.org/en/latest/tutorials/packaging-projects/)

---

# I. Install required packages

Required packages:

- pip
- build: Generating distribution archives
- twine: Uploading the distribution archives

```
    py -m pip install --upgrade pip
    py -m pip install --upgrade build
    py -m pip install --upgrade twine
```

# II. Creating the package files

Put your package files under `src/package_name/`.

```
packaging_tutorial/
├── LICENSE
├── pyproject.toml
├── README.md
├── src/
│   └── package_name/
│       ├── __init__.py
│       └── example.py
└── tests/
```

## 1. README.md

Create a [README.md](https://guides.github.com/features/mastering-markdown) markdown file which will be shown in the PyPI package website.

## 2. LICENSE

Create a license for your package. [link](https://choosealicense.com/)

## 3. pyproject.toml

The pyproject.toml tells build frontend tools like pip and build which backend to use for your project. [link](https://packaging.python.org/en/latest/guides/writing-pyproject-toml/#writing-pyproject-toml)

An example:

```
    [build-system]
    requires = ["hatchling"]
    build-backend = "hatchling.build"

    [project]
    name = "spam-eggs"
    version = "2020.0.0"
    dependencies = [
    "httpx",
    "gidgethub[httpx]>4.0.0",
    "django>2.1; os_name != 'nt'",
    "django>2.0; os_name == 'nt'",
    ]
    requires-python = ">=3.8"
    authors = [
    {name = "Pradyun Gedam", email = "pradyun@example.com"},
    {name = "Tzu-Ping Chung", email = "tzu-ping@example.com"},
    {name = "Another person"},
    {email = "different.person@example.com"},
    ]
    maintainers = [
    {name = "Brett Cannon", email = "brett@example.com"}
    ]
    description = "Lovely Spam! Wonderful Spam!"
    readme = "README.rst"
    license = {file = "LICENSE.txt"}
    keywords = ["egg", "bacon", "sausage", "tomatoes", "Lobster Thermidor"]
    classifiers = [
    "Development Status :: 4 - Beta",
    "Programming Language :: Python"
    ]

    [project.optional-dependencies]
    gui = ["PyQt5"]
    cli = [
    "rich",
    "click",
    ]

    [project.urls]
    Homepage = "https://example.com"
    Documentation = "https://readthedocs.org"
    Repository = "https://github.com/me/spam.git"
    "Bug Tracker" = "https://github.com/me/spam/issues"
    Changelog = "https://github.com/me/spam/blob/master/CHANGELOG.md"

    [project.scripts]
    spam-cli = "spam:main_cli"

    [project.gui-scripts]
    spam-gui = "spam:main_gui"

    [project.entry-points."spam.magical"]
    tomatoes = "spam:main_tomatoes"
```

# III. Generating distributions archives

Run the following command under the directory where `pyproject.toml` is located:

```
    py -m build
```

This command should output a lot of text and once completed should generate two files in the dist directory:

```
    dist/
    ├── example_package_YOUR_USERNAME_HERE-0.0.1-py3-none-any.whl
    └── example_package_YOUR_USERNAME_HERE-0.0.1.tar.gz
```

# IV. Uploading the distribution archives
 
## 1. Upload to TestPyPI 

Upload to TestPyPI for testing and experimentation.

- First register an account on [TestPyPI](https://test.pypi.org/account/register/).
- Create a TestPyPI [API token](https://test.pypi.org/manage/account/#api-tokens), setting the “Scope” to “Entire account”.

Then using the following commands to upload your packages:

```
    py -m twine upload --repository testpypi dist/*
```

You will be prompted for a username and password. For the username, use __token__. For the password, use the **token value**, including the pypi- prefix.

After the command completes, you should see output similar to this:

```
    Uploading distributions to https://test.pypi.org/legacy/
    Enter your username: __token__
    Uploading example_package_YOUR_USERNAME_HERE-0.0.1-py3-none-any.whl
    100% ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 8.2/8.2 kB • 00:01 • ?
    Uploading example_package_YOUR_USERNAME_HERE-0.0.1.tar.gz
    100% ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 6.8/6.8 kB • 00:00 • ?
```

Once uploaded, your package should be viewable on TestPyPI; for example: https://test.pypi.org/project/example_package_YOUR_USERNAME_HERE.

## 2. Upload to PyPI

When the package is ready, you can upload to PyPI instead TestPyPI.

- First register an account on [PyPI](https://pypi.org ).
- Create a TestPyPI [API token], setting the “Scope” to “Entire account”.

Then using the following commands to upload your packages:

```
    twine upload dist/*
```
You will be prompted for a username and password. For the username, use __token__. For the password, use the **token value**, including the pypi- prefix.

Once uploaded, your package should be viewable on PyPI.



