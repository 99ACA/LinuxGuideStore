# Making the configuration more modular and easier to maintain

To organize SSH configuration files using the [***Include***](https://io.adafruit.com/blog/notebook/2016/09/27/ssh-config-includes/) directive, you can split different parts of your SSH configuration into separate files based on their scope.

## Here’s a step-by-step guide on how to achieve this

1. Default SSH Configuration Path

    The default SSH configuration file is located at:

    ```bash
    ~/.ssh/config
    ```

2. Use the Include Directive in the Main Config

    If you want to include several files in a directory (for example, all SSH config files in ~/.ssh/config.d), you can use wildcard patterns.

    ```bash
        touch ~/.ssh/config        
        mkdir ~/.ssh/config.d
        chmod 600 ~/.ssh/config.d/*
    ```

    Then, in your main SSH config file (~/.ssh/config), use:

    ```bash
        # Include all files in the config.d directory
        Include ~/.ssh/config.d/*
    ```

## Example Directory Structure

After organizing the configuration files, your setup might look like this:

```bash
    ~/.ssh/
    ├── config                # Main config file with Includes
    ├── config.d/             # Directory holding split config files
    │   ├── config-personal   # Personal SSH config
    │   └── config-work       # Work-related SSH config
    ├── id_rsa_personal       # SSH private key for personal use
    └── id_rsa_work           # SSH private key for work use
```
