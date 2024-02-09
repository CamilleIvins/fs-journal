#   Jake Overall
***********************
Landing page design
themeforest.net
labartisan.net
github.com/codeworks-template/landing-page

boisecodecamp.com
    live, now, May 4th
#
Simple design that links to complex projects
    want quick load
        no detraction to landing page due to rendering
            - limit animations

This is me
This is what I've done

#NOTE - make name smaller than job title

themeforest.net
    they show what is possible, you decide what is good
# be mindful of people's attention spans
Do not want a clunking landing page - does not rep good design practice
    Click on examples
        - make sure text loads on render - or else no one important will read

You want all images to be kB NOT mB
    web P image is best for loading
    svgs are also good
    mini jpeg is free, too to load pic in

Lighthouse - all but progressive web app checked, then analyze

Pay attention to the built form, not dev server form
    - be careful about speed

Mainly devs like dark screen, most people prefer light

#   Github repo name

NAME IS IMPORTANT
    camilleivins.github.io

index.html
    title
        Hello
    Body -> h1
        'Sup'
Auto enables deploy based on name of repo
    enforce https
CANNOT use .vue extentions
browsers can only read html, css, and js - otherwise the browser CANNOT load

SO 

MUST run "build"
    translate all vue into JS. css, html

run npm -i to get all vue dependencies
npx create-project <<name>> 

npm run serve to start client

meta-tags
    index.html has a list of the meta tags
        parallel a href
            more specific

Source code is not the deliverable code
    this is industry standard
        HOW THINGS ARE ACTUALLY DONE
Github
    settings
        dev settings
            new token
                API token
                    copy exactly, no space, no enter
