# Sidebar widgets

**Topics**

- OroSidebarBundle (adding sidebar widgets)
- OroAsseticBundle (adding assets)
- OroRequireJSBundl (adding javascripts)

**Changes**

```
app
    config.yml (updated, added routs for fos_js_routing)
src/Acme/Bundle/TaskBundle
    Controller
        TaskController (updated, added assignedTasksAction)
    Resources
        config
            requirejs.yml (created)
        messages
            jsmessages.en.yml (created)
        public
            css
                acme.less (created)
            sidebar_widgets
                assigned_tasks
                    js
                        widget.js (created)
                    widget.yml (created)
                
```

## Adding tasks grid to user view page

1. Add Acme/Bundle/TaskBundle/Resources/public/sidebar_widgets/assigned_tasks/widget.yml

  ```
  title: "Assigned Tasks"
    icon: "bundles/acmetask/images/task-icon-small.png"
    module: "acmetask/sidebar/widget/assigned_tasks"
    placement: "both"
    settings:
      perPage: 5

  ```

2. Add Acme/Bundle/TaskBundle/Resources/public/sidebar_widgets/assigned_tasks/js/widget.js

3. Add Acme/Bundle/TaskBundle/Resources/config/requirejs.yml
  
  ```
  config:
    paths:
        'acmetask/sidebar/widget/assigned_tasks': 'bundles/acmetask/sidebar_widgets/assigned_tasks/js/widget.js'
  ```

4. Run commands cache:clear, assets:install and oro:requirejs:build

5. Add Acme/Bundle/TaskBundle/Resources/translations/jsmessages.en.yml

6. Update app/config.yml fos_js_routing: routes_to_expose: [oro_, acme_]

  ```
  fos_js_routing:
    routes_to_expose:         [oro_*, acme_*]
  ```

7. Run commands 

  ```
  app/console fos:js-routing:dump --target web/js/routes.js 
  app/console cache:clear
  ```
  
8. Add Acme/Bundle/TaskBundle/Resources/public/css/acme.less 

9. Add Acme/Bundle/TaskBundle/Resources/public/assets.yml

10. Run commands assets:install abd assetic:dump

11. Ensure that Acme\Bundle\TaskBundle\Controller\Api\Rest\TaskController::getAssignedTasksAction method is used
