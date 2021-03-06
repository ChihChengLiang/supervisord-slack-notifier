supervisord-slack-notifier
==============================================================================

.. image:: https://travis-ci.org/WoLpH/supervisord-slack-notifier.svg?branch=master
  :target: https://travis-ci.org/WoLpH/supervisord-slack-notifier

Event listener for Supervisord that sends notifications to Slack via Web API

Installation
------------------------------------------------------------------------------

.. code-block:: ini

    pip install slack_notifier

Tests
------------------------------------------------------------------------------

Testing is set up using `py.test` and coverage is handled with the `pytest-cov`
plugin.

Run your tests with `py.test` in the root directory.

Coverage is ran by default and is set in the `pytest.ini` file.
To see an html output of coverage open `htmlcov/index.html` after running the tests.

Travis CI
------------------------------------------------------------------------------

There is a `.travis.yml` file that is set up to run your tests for python 2.7
and python 3.2, should you choose to use it.

Set up
------------------------------------------------------------------------------

Add the following to `supervisord.conf`:

.. code-block:: ini

    [eventlistener:slack_notifier]
    command=/path/to/slack_notifier -t=%AUTH_TOKEN% -c=%CHANNEL_NAME% -a
    events=PROCESS_STATE

Options
------------------------------------------------------------------------------

.. code-block::

    -p -- specify a supervisor process_name. Notify when the process goes to
          any of the 'followed' states.  If this process is part of a group, it
          can be specified using the 'process_name:group_name' syntax.

    -a -- Notify about ALL processes.  Overrides any -p
          parameters passed in the same crashmail process invocation.

    -e -- follow only transitions to these events. This overrides event list in
          config.py

    -c -- Channel to send notifications to. Can be either:
          '#public_channel',
          '@private_group',
          'CHANNEL_ID',

    -t -- Web API auth token

The `-p` and `-e` options may be specified more than once, allowing for
specification of multiple processes and events.  Specifying `-a` overrides any
selection of `-p`.


License
------------------------------------------------------------------------------

Released under the MIT License: http://www.opensource.org/licenses/mit-license.php
