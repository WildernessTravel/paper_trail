# Contributing

Thanks for your interest in PaperTrail!

Ask usage questions on Stack Overflow:
https://stackoverflow.com/tags/paper-trail-gem

**Please do not use github issues to ask usage questions.**

On github, we appreciate bug reports, feature suggestions, and pull requests.

## Reporting Bugs

Please use our [bug report template][1].

## Reporting Security Vulnerabilities

Please email jared@jaredbeck.com, batkinz@gmail.com

We will respond as soon as we can. Thank you for responsibly disclosing
security vulnerabilities.

## Development

Install gems with `bundle exec appraisal install`.

Testing is a little awkward because the test suite:

1. Supports multiple versions of rails
1. Contains a "dummy" rails app with three databases (test, foo, and bar)
1. Supports three different RDBMS': sqlite, mysql, and postgres

### Test sqlite, AR 4

```
DB=sqlite bundle exec appraisal ar-4.2 rake

# Run a single test
DB=sqlite bundle exec appraisal ar-4.2 rspec spec/paper_trail_spec.rb
```

### Test sqlite, AR 5

```
DB=sqlite bundle exec appraisal ar-5.2 rake
```

### Test mysql, AR 5

```
DB=mysql bundle exec appraisal ar-5.2 rake
```

### Test postgres, AR 5

```
createuser --superuser postgres
DB=postgres bundle exec appraisal ar-5.2 rake
```

## Adding new schema

Edit `spec/dummy_app/db/migrate/20110208155312_set_up_test_tables.rb`. Migration
will be performed by `spec_helper.rb`, so you can just run rake as shown above.
Also, `spec/dummy_app/db/schema.rb` is deliberately `.gitignore`d, we don't use
it.

## Documentation

### Generate the Table of Contents

```
yarn global add markdown-toc
markdown-toc -i --maxdepth 3 --bullets='-' README.md
```

## Releases

1. Set the version in lib/paper_trail/version_number.rb
1. In the changelog,
  - Replace "Unreleased" with the date in iso-8601 format
  - Add a new "Unreleased" section
1. In the readme, update references to version number, including
  - documentation links table
  - compatability table (major versions only)
1. Commit
1. git push origin 5-stable # or whatever branch
1. Wait for CI to pass
1. gem build paper_trail.gemspec
1. gem push paper_trail-5.0.0.gem
1. git tag -a -m "v5.0.0" "v5.0.0" # or whatever number
1. git push --tags origin

[1]: https://github.com/paper-trail-gem/paper_trail/blob/master/doc/bug_report_template.rb
