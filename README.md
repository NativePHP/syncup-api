# SyncUp API

The backend for **SyncUp**, the chat app built in the **NativePHP Masterclass**. It's a standard Laravel app with [Sanctum](https://laravel.com/docs/sanctum) token authentication, and the mobile app talks to it over HTTP.

The mobile app itself lives in its own repository: [NativePHP/syncup](https://github.com/NativePHP/syncup).

**Sign up for the course:** [nativephp.com/course](https://nativephp.com/course)

## How This Repository Is Organized

Each commit holds the backend work from one video in the course, so you can jump to the state of the API at the end of any video. The backend first appears in the Authentication video.

| Commit message | Video |
|---|---|
| `Authentication` | Sanctum token auth: register, login, logout, and the current user |

## Endpoints

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| `POST` | `/api/register` | None | Create an account and get a token |
| `POST` | `/api/login` | None | Log in and get a token |
| `POST` | `/api/logout` | Bearer token | Revoke the current token |
| `GET` | `/api/user` | Bearer token | Get the logged-in user |

Send an `Accept: application/json` header with every request, so validation errors come back as JSON with a `422` status.

## Getting Started

### Requirements

- PHP 8.3+
- Composer

### Clone and install

```bash
git clone https://github.com/NativePHP/syncup-api.git
cd syncup-api
composer install
cp .env.example .env
php artisan key:generate
php artisan migrate
```

The app uses SQLite by default, so there's no database server to set up.

### Run the API

If you use [Laravel Herd](https://herd.laravel.com), park or link the folder and the API is available at `http://syncup-api.test`. That's the address the course uses, and it works from the iOS simulator because the simulator shares your Mac's network.

A real phone or the Android emulator can't reach `.test` addresses. For those, deploy the API somewhere like [Laravel Cloud](https://cloud.laravel.com), or serve it on your local network:

```bash
php artisan serve --host=0.0.0.0 --port=8000
```

Then use your computer's local IP address (for example `http://192.168.1.20:8000`) as the API's URL.

### Point the app at the API

In the SyncUp app's `.env`, set `API_BASE_URL` to the API's address, including `/api`:

```dotenv
API_BASE_URL=http://syncup-api.test/api
```

## Viewing the API at the End of a Video

1. List the commits (oldest first) to find the one for that video:

   ```bash
   git log --oneline --reverse
   ```

2. Check out that commit using its hash:

   ```bash
   git checkout <commit-hash>
   ```

   Git will say you're in a "detached HEAD" state. That's expected. You're viewing a snapshot, not a branch.

3. Reinstall dependencies and run any new migrations:

   ```bash
   composer install
   php artisan migrate
   ```

4. When you're done, go back to the latest version:

   ```bash
   git checkout main
   ```

To see exactly what a video changed, run `git show <commit-hash>`, or `git show --stat <commit-hash>` for just the list of files.

## Running Tests

```bash
php artisan test
```

## License

SyncUp API is open-source software licensed under the [MIT license](LICENSE.md).
