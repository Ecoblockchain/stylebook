# The Things Network Stylebook

The goal of this project is to contain a shared set of styles and related assets for use on several website properties of [The Things Network](https://www.thethingsnetwork.org). It does not enforce a particular CSS preprocessor or build flow and allows us to adopt global styles step by step.

## Why Less?
The [source stylesheets](src) are in [Less](http://lesscss.org) because it was [the only format](https://csspre.com/convert/) that can be automatically converted to [SCSS](http://sass-lang.com) and [Stylus](http://stylus-lang.com).

## Documentation
The [docs](docs) folder uses [dist/scss](dist/scss) to demonstrate the styles and is a usage example at the same time. You can view the documentation via [GitHub Pages](https://thethingsnetwork.github.io/stylebook/).

## Usage

1. Depend on the repository, e.g. via NPM:

	```bash
	npm install --save thethingsnetwork/stylebook
	```
	
	> You can also [lock in to a certain branch or commit](https://docs.npmjs.com/files/package.json#github-urls).
	
2. Import a stylesheet in the language you use:

	```css
	@import 'ttn/variables';
	
	body {
		color: $ttn-color-brand;
	}
	```
	
	> This example assumes you run Sass with `--load-path node_modules/stylebook/dist/scss` to not have to give the full path on every import.
	
### Stylesheets
There are different strategies for using the stylesheets:

* [dist/*/ttn/variables](dist/less/ttn/variables.less): Just TTN variables. For projects where you want to have full control over the actual styles.
* [dist/*/ttn/ttn](dist/less/ttn/ttn.less): The above plus TTN components.
* [dist/*/ttn/bootstrap-variables](dist/less/ttn/bootstrap-variables.less): TTN and Bootstrap variables. For projects where you'd like to override additional Bootstrap variables before importing (maybe just parts of) Bootstrap.
	* You can import parts of Bootstrap from [dist/*/bootstrap](dist/less/bootstrap). Be aware that the Sass version has components wrapped in another [bootstrap folder](dist/scss/bootstrap/bootstrap).
* [dist/*/ttn/bootstrap](dist/less/ttn/bootstrap.less): All of the above plus all of Bootstrap.
	* This also imports [dist/*/ttn/bootstrap-overrides](dist/less/ttn/bootstrap-overrides.less) for customisations of Bootstrap that cannot be done via variables.

## Development

1. [Install Ruby](https://www.ruby-lang.org/en/downloads/)
2. Install [Bundler](http://bundler.io/):
	
	```bash
	$ gem install bundler
	```

3. Install Ruby dependencies via Bundler:

	```bash
	$ bundle install
	```

4. Install [Node.js and NPM](https://nodejs.org/).

5. Install Node.js dependencies via NPM:

  ```basg
  $ npm install
  ```
  
6. Update styles in [src](src) using [Less](http://lesscss.org).

7. Run `convert` to update [dist](dist) with Less, SCSS, Stylus and CSS versions and process [docs/src](docs/src).

	```bash
	$ npm run convert
	```

> *NOTE:* Running `npm install` will overwrite the git pre-commit hook to execute [npm run convert & npm run add](package.json#L10) automagically on every commit so you can ignore step 7.

## Conventions

* Variables, selectors and mixins should start with `ttn-` so that they do not conflict with other frameworks or custom styles on the site.

## Default variables

Both [Stylus](http://stylus-lang.com/docs/operators.html#conditional-assignment--) and [Sass](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#variable_defaults_) support variable defaults. Less does not and promotes [lazy loading](http://lesscss.org/features/#variables-feature-default-variables) instead. Because we use Less as source to convert to Sass and Stylus this is an issue. So [bin/convert](bin/convert) does has replacements to make all variables in Stylus and Sass defaults, **except** [dist/*/ttn/bootstrap-variables](dist/scss/ttn/_bootstrap-variables.less) so it can use but also override Bootstrap variabls.

## Tests
To run [all tests](test):

```bash
npm install
npm test
```

To update expected with actual output:

```bash
UPDATE=1 npm test
```

## TODO

* Add more base variables.
* Add styles for custom components.
* Include TTN assets logos.
* Maybe even include common templates and scripts?
