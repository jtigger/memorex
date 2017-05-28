

# Gotchas

- if you fail to include the CSRF token in a form, you will get the cryptic message:

    ```
    org.apache.jasper.JasperException: /index.jsp (line: 3, column: 5) Invalid standard action
        org.apache.jasper.compiler.DefaultErrorHandler.jspError(DefaultErrorHandler.java:41)
    ```
