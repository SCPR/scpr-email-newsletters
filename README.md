# SCPR Email Newsletters

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

Core styles are provided in `all.scss`. These styles are loosely based on [Zurb's Responsive Email Templates](http://www.zurb.com/playground/responsive-email-templates), with refactoring made to the markup and CSS in order to add support for Outlook mail clients. 

I've also included Thoughtbot's [Bourbon](http://bourbon.io) which gives you a lean but powerful library of SASS mixins to work with.

### Handling Media Queries

In order to use media queries effectively in email, they need to be preserved in a `<style>` block in the head of the HTML document, while all other css gets inlined into the body. To accomplish this, all media queries live in `layouts/layout.slim`, and include a `data-premailer="ignore"` attribute which tells the Premailer gem to ignore these styles when inlining CSS during the build process.  

## Build

Once you're done with development and ready to inline your CSS, run this command:

`bundle exec rake build`

This will compile all of your templates and CSS, then run everything through Premailer to inline the CSS. We're using an SCPR-forked version of the Premailer gem in order to add support for Premailer ignoring media queries during the build process. 

The results of the build process are located in the imaginatively-named `build` directory, and include a .zip file of the entire package.

## Post-build

Each build template needs to be uploaded into Eloqua (or integrated in a separate project if you're sending emails via the Eloqua API). Since Eloqua injects its own email footers as global files, you'll need to manually remove the Global Footer markup from the code before uploading to Eloqua or sending the API.

## Todo

-- Refactor all SASS; shit's a mess right now and needs to be parsed out into a sensible files structure, commented, and DRY-ed up.
-- Extract the core project into a public repository that could be used for any email front-end dev project.
