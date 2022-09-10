# Effective Java Section 4 Item 15

## Minimize the accessibility of classes and members

four possible access levels, listed here in order of increasing accessibility:

- *private—*The member is accessible only from the top-level class where it is declared.

- *package-private—*The member is accessible from any class in the package where it is declared. Technically known as default access, this is the access level you get if no access modifier is specified (except for interface members, which are public by default).

- *protected—*The member is accessible from subclasses of the class where it is declared (subject to a few restrictions [JLS, 6.6.2]) and from any class in the package where it is declared.

- *public—*The member is accessible from anywhere.

Tags :
```
#java #public #private #package #default #access_level
```
