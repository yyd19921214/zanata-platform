# Make is used here so that we can suppress script execution in other packages
# with --ignore-scripts, but not have to manually add --ignore-scripts=false to
# each invocation of `yarn run <command>`.
# Instead we can just invoke `make <command>`.
# We also get tab-completion of the make commands.

# Ensure all dependencies are present at appropriate versions.
install:
	yarn --ignore-scripts

# Build the css and javascript bundles using webpack.
# Files end up as *.css *.js files ./dist
build:
	yarn build --ignore-scripts=false

draft:
	yarn draft --ignore-scripts=false

watch:
	yarn watch

# Run the app on a local development server, automatically rebuild and refresh
# when the code changes (sprites are only built at the beginning).
watch-editor:
	yarn watch:editor

styleguide-build:
	yarn styleguide-build --ignore-scripts=false

styleguide-server:
	yarn styleguide-server --ignore-scripts=false

# Run react-storybook server for development and testing of React components
# specific to the editor.
storybook-editor:
	yarn storybook-editor

# Run react-storybook server for development and testing of React components
# for everything except the editor.
storybook-frontend:
	yarn storybook-frontend

# Build a static version of the React component storybook
#  - outputs to ./storybook-static
#  - will not display properly from file:// url since it uses an iframe
#  - includes everything from /app/build even though it does not need
#    it all (only needs icons.svg at this point). Not worth the extra complexity
#    to prevent that.
storybook-static:
	yarn build-storybook --ignore-scripts=false

# Run the script to create boilerplate for a new component.
component:
	node ./scripts/codemods/create-component.js

# Run the tests.
test:
	yarn test

# Run the tests on every change
# Specify coverage=path if you want to limit reported coverage scope. This is
# useful when using pattern mode to limit the tests that are run.
# e.g. make test-watch coverage="app/editor/reducers/*"
#      p > app/editor/reducers/.*
# NOTE coverage uses a glob pattern (*), but test pattern uses a regex (.*)
test-watch:
ifdef coverage
	yarn test:watch -- --collectCoverageFrom=$(coverage)
else
	yarn test:watch
endif

# Run a server that implements some of the Zanata API with some dummy data.
# The server runs on localhost:7878 and has 0.5 to 5s of random latency.
fakeserver:
	cd node_modules/fake-zanata-server && yarn start

# Run a local development server backed by a fake Zanata server
watch-fakeserver:
	${MAKE} -j2 watch fakeserver

.PHONY: test build
