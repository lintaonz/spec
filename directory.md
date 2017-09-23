# Project directory structure specification


## Introduction

The main design goal of the document is that the project structure of the project development is consistent, making it easy to understand and facilitate the construction and management.

### Claim

In this document, the keywords used will be indicated by the Chinese keyword enclosed in Chinese brackets: MUST. The keywords "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" are defined in rfc2119 

### specification specification agreement

In the following specification document:

1. The `project 'contains but is not limited to` business items' and `package items'.
2. `$ {root}` represents the root of the `project '.

<a name="restype"> </a>

## resource classification

`Resources` divided into two categories:

1. `source code resources`: refers to the developer to write the source code, including `js`,` html`, `css`,` template` and so on.
2. ${root} represents the root of the project.


## directory naming principle

1. simple. Have the habit of abbreviated words * must (MUST) * use easy to understand the abbreviation. Such as: source code directory using `src`, do not use` source`. Here are some examples:
    1. `img`: picture. * Not allowed (MUST NOT) * use `image`,` images`, `imgs` etc.
    2. `js`: javascript script. * Not allowed (MUST NOT) * Use `script`,` scripts` and so on.
    3. `css`: style sheet. * Not allowed (MUST NOT) * use `style`,` styles` and so on.
    `` Swf`: flash. * Not allowed (MUST NOT) * Use `flash` and so on.
    5. `src`: source file directory. * Not allowed (MUST NOT) * Use `source` and so on.
    6. `Dep`: Introduces the third party dependent package directory. * Not allowed (MUST NOT) * use `lib`,` library`, `dependency` etc.
2. * not allowed (MUST NOT) * use the plural form. Such as: `imgs`,` docs` is not allowed.



## directory division

<a name="root"> </a>
### $ {root} directory structure

In the case of $ {root}, the directory structure * MUST * is divided by `function '* * MUST NOT * The directory of` resource type' or `business logic` is placed directly on $ {root} under.

Commonly used directories are `src`,` doc`, `dep`,` test` and so on. For more information, please refer to [Level 1 Descriptions] (# level1)

    $ {root} /
        src /
        test /
        doc /
        dep /
        ...

### Business project directory structure

`$ {Root} directory structure of the business project follows the [$ {root} directory structure] (# root).


#### Project code

Business item * Yes (SHOULD) * A code name for the project. Code Name * Must (MUST) * for a word, should not be too long. Example: Beidou project code for the `triones`, Columbus project code-named` clb`, Baidujian the project code-named `jn`. The project code is useful for distinguishing between different projects and leaving an expanded posterior for the reuse of future projects.

During project development, the following [Loader Configuration] (module.md # config) is usually used to point the project code to `src`.

`` `javascript
{
    baseUrl: '$ {docroot}',
    paths: {
        'triones': 'src'
    }
}
`` ``


#### According to the business logic division src directory structure

The subdirectories (eg `biz1` in [example] (# bizdirexample) are called` business directories'.

`src` * must (MUST) * only contain` business directory `and` common` directory. `Business public resource` * must (MUST) * be named `common`. `` `` `` `` `` `` `` `` `` `` `` `` `` `` `` `` `` `` `` `` `` `` `` `` `` `` `` `` `

    $ {root} /
        src /
            common /
            biz1 /
                subbiz1 /
                subbiz2 /
            biz2 /

Smaller `business items` (such as the delivery side), `src` directory allows the directory as a` business directory ', directly in accordance with [business directory division principle] (# bizdirprinciple).

    $ {root} /
        src /
            foo.js


<a name="bizdirprinciple"> </a>
#### Business directory division principle

1. `JS resource` * not allowed (MUST NOT) * by `resource type` partition directory, * must (MUST) * by `business logic` directory. `JS resources` should be placed directly under `business directory '. That is: `business directory` does not allow the `js` directory.
2. In addition to That is: `business directory` to allow `css`,` tpl` directory.
3. That is: `business directory` to allow `` img`, `swf`,` font` directory.
4. For example: `subbiz1` in the following example.


Typically, for a `business directory ', * encourage (SHOULD) * will be business-related` source file resources `are placed directly under the` business directory'.

    biz1 /
        img /
            add_button.png
        add.js
        add.tpl.html
        add.css

`Business directory Should it be sub-business, the establishment of sub-business directory?

    biz2 /
        subbiz1 /
            Points Points United:1 Finds.aintitherites:1:1 United:1 United States Find automobiles Finds.:1
            list.tpl.html
            list.css
        subbiz2 /

Encourage (MAY) * will be non-`JS resources` by `resource type` directory management to manage.

    biz1 /
        css /
            add.css
            edit.css
            remove.css
            img /
                add_button.png
        tpl /
            add.html
            Find composition views United States draft Find Copyright Decision Copyright Copyright Chinese Copyright
            Find outcome Results:1:1:1:1:1:1:1:1:1:1:1:1:1:1:1:1 composition
        add.js
        edit.js
        remove.js


(#bizdir) section.


<a name="bizdirexample"> </a>
#### Example of business project directory partitioning

    $ {root} /
        src /
            common /
                img /
                    sprites.png
                    logo.png
                conf.js
                layout.css
            biz1 /
                img /
                    add_button.png
                add.js
                add.tpl.html
                add.less
            biz2 /
                subbiz1 /
                    list.js
                    list.tpl.html
                    list.css
                subbiz2 /
        dep /
            er /
                src /
                test /
            esui /
                src /
                Decision
        Decision
        doc /
        Decision drafts strats. Decision
        main.html
        ...

<a name="packagedir"> </a>
### package project directory structure

`$ {Root} directory structure of the package project follows the [$ {root} directory structure) (# root).

<a name="packagesrc"> </a>
#### package item src directory structure division

In accordance with the usual understanding, a `package item 'should not be particularly complicated.

Therefore, the 

    $ {root} /
        src /
            css /
                img /
                    sprites.png
                table.css
                button.css
                select.css
            main.js
            Control.js
            InputControl.js
            Button.js
            Table.js
            Select.js
        test /
        doc /
        package.json
        ...




## common directory

<a name="level1"> </a>

### Level 1 directory

Directly placed in the `$ {root}` under the directory called `first-level directory`. Level directory * must (MUST) * have some kind of `function 'attribute.

In addition to some of the common directories listed below, `$ {root}` can also place files related to project releases, such as `build.sh`,` build.xml`, `Makefile`,` Gruntfile`, etc. The

#### src

The `src` directory is used to store the source files at the time of development. * * MUST * is deleted at the time of publication.


#### dep

The contents of this directory are managed by the platform tool, and the project developer * MUST NOT * changes any of the third party packages in the `dep` directory.

When the project needs to modify the introduction of third-party code, the third-party package should be directly placed in the `$ {root} / src` directory, the rules see the provisions of the directory.

For more information on `package 'please refer to [package structure specification] (package.md)


#### tool

The `tool` directory is used to store the tools used at the time of development or build. The directory must be deleted at the time of publication *.


#### test

The directory must be deleted at the time of publication *.


#### doc

The `doc` directory is used to store project documents. The project document may be a document that the developer maintains, or it may be a document generated by the tool.


#### entry

`entry` directory is used to store the` page entry file 'of the project, usually a static page that can be accessed directly after going online.

`RIA project

    $ {root} /
        src /
            common /
                conf.js
            card /
            gold /
            message /
        index.html
        main.html
        ...


`Multi-page project` 

    $ {root} /
        src /
            common /
                conf.js
            card /
            gold /
            message /
        entry /
            card.html
            gold.html
            message.html
            ...


When the project is published, the build tool can parse and compile the entry for the page entry file.


`RIA project` After compiling the build tool, the directory structure might look like this:

    output /
        asset /
            js /
            css /
            tpl /
            img /
        index.html
        main.html

`Multi-page project` After compiling the build tool, the directory structure might look like this:

    output /
        card /
            asset /
                js /
                css /
                img /
            index.html
        gold /
            asset /
                js /
                css /
                img /
            index.html

#### asset

The `asset` directory is used to store static resources for` online access'.

Often the build tool will parse, merge, and compress the resources under the `src` directory and the` dep` directory, and generate them into the `asset` directory. So the directory to avoid manual management. The following is an example of the `asset` directory after the builder builds:

    $ {root} /
        asset /
            js /
                loader.js
                build.js
            css /
                common.css
                img /
            tpl /
                build.tpl.html
            img /
            ...

<a name="resdir"> </a>


### resource catalog

The directory named by the `resource 'type is called the` resource directory'. `Resource directory` * not allowed (MUST NOT) * directly under $ {root}.


#### js

The `js` directory can be used to store the` js` resource file (including the `coffeescript` and other languages ​​that can be compiled into` js`). `js` file suffix name * must (MUST) * for .js,` coffeescript file `suffix name * must (MUST) * for .coffee.

`js` directory * must (MUST) * store the` js` resource file, but the `js` resource file is not necessarily (MAY NOT) stored in the` js` directory:

1. For the `src` directory, the` js` resource file * does not allow (MUST NOT) * is stored in the `js` directory.
2. For the `asset` directory, the` js` resource file * (SHOULD) * is stored in the `js` directory, depending on the build behavior.
3. For other `first-level directories',` js` resource files * can (SHOULD) * not stored in the `js` directory.

#### css

The `css` directory can be used to store` css resource files' (including dynamic stylesheet languages ​​such as `less`,` sass`). 

1. For the `src` directory, the` css` resource file * can (SHOULD) * be stored in the `business directory 'and * (SHOULD) * in the` css` directory.
2. For the `asset` directory, the` css` resource file * can be (SHOULD) * stored in the `css` directory, depending on the build behavior.
3. For other `first-level directories',` css` resource files * can (SHOULD) * not stored in the `css` directory.

Refer to the [img] (# imgdir) section for a description of the location of css reference pictures.


<a name="imgdir"> </a>

#### img

The `img` directory can be used to store` picture resource files'. Including Common picture resources are `gif / jpg / png / svg / bmp` and so on.


For `page direct reference to` picture:

1. Pictures that are referenced by multiple pages * SHOULD * are placed in the `$ {root} / src / common / img` directory.
2. a single page reference picture * should (SHOULD) * in the `. / Img` directory,` .` on behalf of the current page where the directory.


#### tpl

The `tpl` directory can be used to store the` template` resource file. `template` resource file suffix name * can (SHOULD) * for` .html` or `.tpl`.

Typically, for the `RIA` system, the` template` resource file uses the `.html` suffix so that it can be loaded by` xhr`.


#### font

The `font` directory can be used to store font resource files. Common font resources are `tff / woff / svg` and so on.


#### swf

`swf` directory can be used to store` flash` resource files. 


<a name="bizdir"> </a>

### Business directory

<a name="commondir"> </a>

#### common

The `common` directory is the business public directory, which is used to store business documents for business projects. So, when the directory structure is organized according to `business logic ', the business logic is named * MUST NOT * is` common`.


## FAQ

### Why biz below no resource type catalog?

If you continue to divide the `resource directory 'under` biz`, the structure of the code might be like this:

    $ {root} /
        src /
            biz1 /
                js /
                    list.js

When we need to use `list.js`, we must write the following code:` require ("../biz1 / js / list") `, but logically, the more reasonable wording should be` require (" ../biz1 / list ")`. So we do not recommend dividing the source directory under `biz`.
