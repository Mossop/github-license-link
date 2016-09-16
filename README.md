# github-license-link

This Github webhook listens for new pull requests created by new contributors to
your project and prompts them to go and look at your contribution guidelines.

A new contributor is defined as a user who isn't a member of the organisation
the repository belongs to or isn't the owner of the repository.

Once the contributor posts a commenting uncluding the string "I understand" they
will no longer see the message in that repository.

## Setup

Deploy this node app somewhere and set a few environment variables:

    PORT=<port to listen on>
    GITHUB_TOKEN=<Github token for a user to post as>
    MONGODB_URI=<Mongo DB instance to use>

Then set up a webhook on any Github repositories you want monitored to point to
it:

    https://<app url>/github

The message the webhook posts in the pull request is configurable and is taken
from the templates directory. The webhook first looks for
`templates/<org>/<repo>/response` and then for `templates/<org>/response` and
then for `templates/response`. The first found is posted as the first comment
to new pull requests.

## Testing

In order to test you must first set up a working mongo database. Docker is an
easy way to accomplish this. Once running set an environment variable to point
to it and then run the tests:

    export MONGODB_URI=mongodb://192.168.99.100:32768/mozilla-licensing
    npm test
