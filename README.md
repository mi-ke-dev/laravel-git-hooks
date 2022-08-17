## Continuous Integration For Laravel project

The purpose of this repo is to provide step-by-step guidelines to install pre-commit git hooks for other projects.

The pre-commit githooks described here will do the following:

- Perform source code static analysis using Laravel Pint to look for common issues
- Look for forbidden functions that might lead to performance loss or increased billing
- Enforce commit message guidelines, using Conventional Commits

## Steps

Install CaptainHook, Laravel Pint, PHP CodeSniffer, and Conventional Commits

```
composer require --dev captainhook/captainhook
composer require --dev laravel/pint
composer require --dev squizlabs/php_codesniffer
composer require --dev ramsey/conventional-commits
```

See https://github.com/ramsey/conventional-commits#configuration-in-a-separate-file and then update your `composer.json`

```
  "extra": {
        // ...,
		"ramsey/conventional-commits": {
			"configFile": "./conventional-commits.json"
		}
	}
```

Copy CI configuration files

```
cp captainhook.json ~/my-project-root/captainhook.json
cp conventional-commits.json ~/my-project-root/conventional-commits.json
cp phpcs.xml ~/my-project-root/phpcs.xml
cp pint.json ~/my-project-root/pint.json
```

Run `vendor/bin/captainhook install`

```
vendor/bin/captainhook install

	Install 'commit-msg' hook? [Y,n] y			# 👈
	'commit-msg' hook installed successfully

	Install 'pre-push' hook? [Y,n] n

	Install 'pre-commit' hook? [Y,n] y			# 👈

	The 'pre-commit' hook exists! Overwrite? [y,n] y	# 👈
	'pre-commit' hook installed successfully

	Install 'prepare-commit-msg' hook? [Y,n] y		# 👈
	'prepare-commit-msg' hook installed successfully

	Install 'post-commit' hook? [Y,n] n

	Install 'post-merge' hook? [Y,n] n

	Install 'post-checkout' hook? [Y,n] n

	Install 'post-rewrite' hook? [Y,n] n
```

## Preparing a commit message

You can prepare a simple commit message via `git commit -m "type(scope): what was changed"`

If you need to prepare a commit message that is more elaborate, you can use the helper:

``./vendor/bin/conventional-commits prepare`
