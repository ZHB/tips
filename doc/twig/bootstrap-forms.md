Forms displayed as a Bootstrap style in sf app
=================

In ``app/config/parameters.yml`` file :

```yml
twig:
    form_themes:
        - form/bootstrap_3_layout.html.twig
```

Checkboxes on multiple columns
--------------

Add your custom form theme that extends from Symfony bootstrap_3_layout.html.twig.

For a 3 columns display, override the choice_widget_expanded widget :

```twig
{% block choice_widget_expanded %}
    <div {{ block('widget_container_attributes') }}>
        {%- for row in form|batch(3) %}
            <div class="row">
                {% for child in row %}
                    <div class="col-md-4">
                        {{- form_widget(child, {
                            parent_label_class: label_attr.class|default(''),
                            translation_domain: choice_translation_domain,
                        }) -}}
                    </div>
                {% endfor %}
            </div>
        {% endfor -%}
    </div>
{% endblock choice_widget_expanded %}
```