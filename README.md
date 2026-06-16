# LinkTree Clone

A simple link-in-bio app where users sign up, manage their own links, and share a public profile page at `/:username`. Built as a learning project to practice Rails CRUD, RESTful routing, and user authentication.

## Tech Stack

- **Language:** Ruby 4.0.5
- **Framework:** Ruby on Rails 8.1
- **Database:** MySQL
- **Authentication:** Devise
- **Frontend:** Hotwire (Turbo + Stimulus), Tailwind CSS, ERB views
- **API / JSON:** Jbuilder (optional `.json` responses on link routes)
- **Testing:** Minitest, Capybara, Selenium WebDriver
- **Other:** RESTful resources, Propshaft, Import maps, Puma, Docker, Kamal, GitHub Actions

## Features

- User sign-up and login with Devise (username + email)
- Full CRUD for links (create, read, update, delete) scoped to the logged-in user
- Public profile page at `/:username` showing that user's links (no login required)
- RESTful `resources :links` routes with HTML and JSON response formats
- Tailwind-styled UI with Turbo-driven interactions
- CI pipeline with security scans, linting, and automated tests

## Getting Started

### Prerequisites

- Ruby 4.0.5 (see `.ruby-version`)
- MySQL 5.6.4+ installed and running
- Bundler (`gem install bundler`)

### Installation

```bash
git clone https://github.com/aDominga/LinkTreeClone.git
cd LinkTreeClone
bundle install
```

Create the MySQL user and databases (adjust names to match `config/database.yml` if needed):

```bash
mysql -u root -p -e "CREATE USER IF NOT EXISTS 'l_tree_user'@'localhost' IDENTIFIED BY 'your_password';"
mysql -u root -p -e "CREATE DATABASE IF NOT EXISTS l_tree_ro_r_development;"
mysql -u root -p -e "CREATE DATABASE IF NOT EXISTS l_tree_ro_r_test;"
mysql -u root -p -e "GRANT ALL PRIVILEGES ON l_tree_ro_r_development.* TO 'l_tree_user'@'localhost';"
mysql -u root -p -e "GRANT ALL PRIVILEGES ON l_tree_ro_r_test.* TO 'l_tree_user'@'localhost';"
```

Prepare the database and start the app:

```bash
export DB_PASSWORD=your_password
bin/rails db:prepare
bin/dev
```

Visit [http://localhost:3000](http://localhost:3000).

Or run the full setup script (installs gems, prepares the DB, and starts the dev server):

```bash
export DB_PASSWORD=your_password
bin/setup
```

### Environment Variables

Set these in your shell before running the app (or add them to a `.env` file if you use a loader like `dotenv-rails`):

| Variable | Required | Description |
|----------|----------|-------------|
| `DB_PASSWORD` | Yes (dev) | MySQL password for `l_tree_user` |
| `DB_USERNAME` | No | MySQL username (default: `l_tree_user`) |
| `DB_HOST` | No | MySQL host (default: `127.0.0.1`) |
| `DB_PORT` | No | MySQL port (default: `3306`) |
| `RAILS_MASTER_KEY` | Production | Decrypts `config/credentials.yml.enc` |
| `L_TREE_RO_R_DATABASE_PASSWORD` | Production | MySQL password for the production database |

Example for local development:

```bash
export DB_PASSWORD=your_password
export DB_USERNAME=l_tree_user
export DB_HOST=127.0.0.1
export DB_PORT=3306
```

### Running Tests

```bash
export DB_PASSWORD=your_password
bin/rails db:test:prepare
bin/rails test
```

### Useful Commands

| Command | Description |
|---------|-------------|
| `bin/dev` | Start Rails server + Tailwind CSS watcher |
| `bin/rails console` | Open Rails console |
| `bin/rails routes` | List all application routes |
| `bin/rubocop` | Run linter |
| `bin/brakeman` | Run security scan |

## Project Structure

| Path | Purpose |
|------|---------|
| `app/controllers/links_controller.rb` | Link CRUD and public profile logic |
| `app/models/` | `User` and `Link` Active Record models |
| `config/routes.rb` | REST routes, Devise auth, public `/:username` profile |
| `app/views/links/` | HTML views and Jbuilder JSON templates |
| `db/schema.rb` | Database schema |

## Deployment

This app includes a `Dockerfile` and Kamal config (`config/deploy.yml`) for containerized deployment. See the [Kamal documentation](https://kamal-deploy.org/) for production setup details.

## License

This project is open source and available for learning purposes.
