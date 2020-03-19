# evote-movie-2020-03-front-controller

- move all display pages into new folder `/templates`

- move images and css into new folder `/public`

- create `composer.json` to define PHP namespaced `Tudublin` classes in `/src`

    ```json
    {
      "autoload": {
        "psr-4": {
          "Tudublin\\":"src"
        }
      }
    }
    ```

- generate `vendor` folder and autoloader by runing `composer dump-autoload`

- add root website script `/public/index.php` to read and run autoloader, and create `WebApplication` object and invoke `run()` method
    
    ```php
    <?php
    require_once __DIR__ . '/../vendor/autoload.php';
    
    use Tudublin\WebApplication;
    
    $app = new WebApplication();
    $app->run();
    ```

- change all navigation links to the form `/index.php?action=<PAGE>`

    - e.g. `/index.php?action=about` for link to about page

    ```html
    <nav>
        <ul>
            <li>
                <a href="/" class="current_page">Home</a>
            </li>
    
            <li>
                <a href="/index.php?action=about">About Us</a>
            </li>
    ```
- create `src` folder to contain classes `WebApplication` and `MainController`

- create `WebApplication` class to test for value of `GET` variable `action` and choose which `MainController` method to invoke

    ```php
    class WebApplication
    {
        public function run()
        {
            $action = filter_input(INPUT_GET, 'action');
            $mainController = new MainController();
    
            switch ($action) {
                case 'about':
                    $mainController->about();
                    break;
    
                case 'contact':
                    $mainController->contact();
                    break;
    ```

- create `MainController` class with methods to display each of the page templates

    ```php
    class MainController
    {
        public function home()
        {
            require_once __DIR__ . '/../templates/index.php';
        }
    ```

- create `composer.json` to define PHP namespaced `Tudublin` classes in `/src`

    ```json
    {
      "autoload": {
        "psr-4": {
          "Tudublin\\":"src"
        }
      }
    }
    ```
