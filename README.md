PDF2Nook
=========

PDF2Nook is a Ruby-based CLI tool designed to convert regular PDF files and make them more readable on Barnes & Nobel Simple Touch Nook reader and maybe some other small 6-inch e-ink readers…

What PDF2Nook actually does
-----------

  - reads PDF book from the original file
  - splits every single page into the top and bottom parts
  - rotates pages to landscape format (90 or 270 degrees to match page turn buttons)
  - trims pages' empty margins to increase small fonts readability
  - converts pages to grayscale colorspace
  - increases pages' contrast to make text more readable
  - resizes pages to fit reader screen density (actually 167 DPI for Nook)
  - exports all pre-rendered pages to a new PDF file ready to read on Nook

What it looks like
-----------

Not readable PDF page in portrait mode:

![Not readable PDF page in portrait mode…](http://i.imgur.com/3TG53.png "Not readable PDF page in portrait mode…")

Converted to two more readable pages in landscape mode with preservation of key bindings:

![More readable PDF page in landscape mode…](http://i.imgur.com/XuBxf.png "More readable PDF page in landscape mode…")

![More readable PDF page in landscape mode…](http://i.imgur.com/iI3Ry.png "More readable PDF page in landscape mode…")


Dependencies
-----------

Under the hood PDF2Nook uses a bunch of tools and libraries to work with PDF and to make all this kind of magic, so it has some dependencies:

  - [**RMagick**](http://rmagick.rubyforge.org/) — Ruby ImageMagick® and GraphicsMagick binding, the heart of tool
  - [**Clamp**](https://github.com/mdub/clamp) — easy to use and quite flexible Ruby CLI framework for command-line interface
  - [**Ruby-progressbar**](https://github.com/jfelchner/ruby-progressbar) — a customizable text progress bar Ruby library to indicate rendering
  - [**Rainbow**](https://github.com/sickill/rainbow) — a little but pretty useful Ruby tool-library for pretty printed CLI output

Installation
-----------

To install PDF2Nook just run:
`[sudo] gem install pdf2nook`

In addition, if you had any problems with building native extension for RMagick, try installing the following stuff (tested on Ubuntu 12.04) and reattempt PDF2Nook installation after that:

    sudo apt-get install ruby1.9.3
    sudo apt-get install librmagick-ruby libmagickcore-dev libmagickwand-dev
    sudo gem install rmagick

or following on OS X:

brew install imagemagick

Usage
-----------

    pdf2nook.rb [OPTIONS] PATH

    Parameters:
        PATH                          PDF file path to convert it

    Options:
        -c, --colors COLORS           output grayscale colors count (default: 16)
        --rotate                      set this flag if you set up your bottom buttons to flip pages forward
        --cleanup                     set this flag if you want to clear tmp files after converting
        -h, --help                    print help

Examples
-----------

+ The easiest way to convert a book is to execute this command:
`$ pdf2nook ./book_name.pdf` — it will process your file with default settings and put the result right in the same folder as your original file, named as `nook_book_name.pdf`

+ To cleanup temporary files after converting, just add `--cleanup` flag:
`$ pdf2nook --cleanup ./book_name.pdf`

+ If you prefer to set your Nook to flip pages forward with the bottom hardware button and back with the top button, set the `--rotate` flag to rotate landscape pages to the proper side:
`$ pdf2nook --cleanup --rotate ./book_name.pdf`

+ To change default colors count of the output pages, use `--colors`  option like this:
`$ pdf2nook --cleanup -c 256 ./book_name.pdf`


Known issues
-----------
Here I want to note the known problems. Some of them I will try to fix in the future, but some of them do not seem so problematic, to complicate the code because of them and invent bicycles…

* **Clipped lines** (see screenshots above) — the algorithm of bisection is quite simple and stupid. It just cuts the page right in the middle no matter whether there is some content or not. If the mean happens to go through a text line or an image, it will split that content. It seems a big deal, but I know that human brain can recognize text even split in halves, so just use your brain and leave the machine alone, you'll see, it's not really hard to do.

* **Different scales of trimmed pages** (see screenshots above) — pages could be trimmed in using different scales because of padding of footer or header or side column typographic elements, such as page numbers, information blocks and text boxes located outside of the main paragraphs layout. But at the same time blank edges trimming is an important part of improving readability of the text.

* **High CPU and memory usage** — your machine can become quite slowly while the tool is processing your file. Be patient and if you can, just let it do its thing, to get quickest result with no annoyance.

* **There is no magic** — if your PDF book is get up using a terribly microscopic font size or scanned with low quality, PDF2Nook will not be able to make it better, I'm sorry.

Help and contribution
-----------
As you can see, English and even Ruby are not my native languages :) So I understand that here I might have a ton of mistakes and stylistic problems. I will be very grateful to get any assistance with typo and grammar correction in README. And it will make it even happier if I get your help with improvement of code quality for the output pdfs. So feel free to make Pull requests and/or bug report issues.

Contributing to pdf2nook
-----------

* Check out the latest master to make sure the feature hasn't been implemented or the bug hasn't been fixed yet.
* Check out the issue tracker to make sure someone already hasn't requested it and/or contributed it.
* Fork the project.
* Start a feature/bugfix branch.
* Commit and push until you are happy with your contribution.
* Make sure to add tests for it. This is important so I don't break it in a future version unintentionally.
* Please try not to mess with the Rakefile, version, or history. If you want to have your own version, or is otherwise necessary, that is fine, but please isolate to its own commit so I can cherry-pick around it.


Special thanks
-----------

* Vera Surkova (https://github.com/surkova) for the spelling and translation.


Copyright
-----------

Copyright (c) 2012 Smile @rT. See LICENSE.txt for further details.
