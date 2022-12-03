# The Purpose of @ConditionalOnProperty

Typically, when developing Spring-based applications, **we need to create some beans conditionally based on the presence and value of a configuration property.**

For example, we may want to register a DataSource bean to point to a production or test database depending on if we set a property value to “prod” or “test.”

Fortunately, achieving this isn't as hard as it might look upon first glance. The Spring framework provides the @ConditionalOnProperty annotation precisely for this purpose.

In short, the @ConditionalOnProperty enables bean registration only if an environment property is present and has a specific value. By default, the specified property must be defined and not equal to false.

Now that we're familiar with the purpose of the @ConditionalOnProperty annotation, let's dig deeper to see how it works.

**Related**:
```
#java #spring #conditionalOnProperty
```
**Links**:
```
https://www.baeldung.com/spring-conditionalonproperty
```
