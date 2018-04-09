# Traklight PHP API Wrapper

This is a simple PHP wrapper for the [Traklight](https://www.traklight.com/) API. This wrapper supports creating users and auto-logging users into their Traklight dashboard.

## Usage
### Initialize Wrapper

    $tk = new TraklightApiWrapper('your_subdomain','your_auth_key');
    $tk->useStaging = true;  # Optionally use Traklight test server

### Retrieve all users from your sub-domain

    $users = $tk->getUsers();
    var_dump($users);

### Retrieve a specific user from your sub-domain

    $user = $tk->getUser('user_id');
    var_dump($user);

### Create a user on your sub-domain
    $user = $tk->createUser(Array(
      'email'        => 'joe@example.com',   # required
      'firstName'    => 'Joe',               # required
      'lastName'     => 'Example',           # required
      'timeZone'     => 'America/Phoenix',   # optional  default "UTC"
      'password'     => 'foobarFB1',         # required
      'phoneNumber'  => '555-555-555',       # optional  default "555-555-5555"
      'postalCode'   => '85003',             # optional  default "00000"
      'countryCode'  => 'US',                # required
    ));
    var_dump($user);

- **timeZone** - must be a value from the [tz database](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)
- **password** - minLength=8, minNumLower=1, minNumUpper=1, minNumDigit=1
- **countryCode** - must be 2 character ISO code

### Automatically log a user into their Traklight Dashboard

    <?php $url = $tk->getSessionUrl('joe@example.com'); ?>
    <iframe
	id="traklight_iframe"
	style="height: 100%; width: 100%"
	src="<?= $url ?>"
	name="traklight_app"
	sandbox="allow-same-origin allow-forms allow-scripts allow-popups allow-top-navigation"
	seamless>
    </iframe>
