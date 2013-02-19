# KPCC Email Newsletters

A simple project, built on top of [Middleman](http://middlemanapp.com/), for coding up HTML emails using all the modern front-end hotness (SASS, ERB, Slim) then compiling things down into CSS-inlined, road-hardened templates ready for the cold, cruel world of email clients. 

## Installation

Clone

`$ git clone git@github.com:SCPR/kpcc-email-newsletters.git`

Install Dependencies

`$ bundle install`

Power up a server

Either set up the project to use Pow, or run the Middleman development server:

`bundle exec middleman server`

## Development

### Templates

### Stylesheet Authoring

Core styles are provided in `all.scss`. These styles are based on [Zurb's Responsive Email Templates](http://www.zurb.com/playground/responsive-email-templates).

I've also inclouded Thoughtbot's [Bourbon](http://bourbon.io) which gives you a lean but powerful library of SASS mixins to work with.

### Handling Media Queries

## Build

Once you're done with development and ready to inline your CSS, run this command:

`bundle exec rake build`

This will compile all of your templates and CSS, then run everything through Premailer to inline the CSS. We're using an SCPR-forked version of the Premailer gem in order to add support for Premailer ignoring media queries during the build process. 

The results of the build process are located in the imaginatively-named `build` directory, and include a .zip file of the entire package.

## Post-build

Each build template needs to be uploaded into Eloqua, most likely created as a template. Since Eloqua manages the email headers and footers as global files, you'll need to manuall remove the Global Header and Footer markup from the code before uploading to Eloqua.

## Todo

-- Refactor all SASS; shit's a mess right now and needs to be parsed out into a sensible files structure, commented, and DRY-ed up.
-- Extract the core project into a public repository that could be used for any email front-end dev project.