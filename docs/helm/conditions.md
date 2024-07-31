# Conditions

In helm, conditions are the same as other languages. This will help us to evaluate the conditions, and based on the output,
we can take the decision.

Example: If conditions.

In helm, if the value is available in the `values.yaml` file, then it will update it in the manifest files. In case, 
if the value is not available in the `values.yaml`, we can ignore that field and create the manifest files without that field.
To do so, we can use if conditions.

Let us assume that in our nginx chart, we have a service manifest file which has labels. This label needs to be picked up 
from `values.yaml`.

`values.yaml`

![helm_37.png](../assets/helm_37.png)

`service.yaml`

```html

apiVersion: v1
kind: Service
metadata:
  name: {{ .Release.Name }}-service
  labels:
    environment: {{ .Values.environment }}
spec:
  type: {{ .Values.service.type }}
  selector:
    app.kubernetes.io/name: MyApp
  ports:
    - port: {{ .Values.service.port }}
      targetPort: {{ .Values.service.port }}
      nodePort: 30007
```

Let us install the helm chart now.

![helm_38.png](../assets/helm_38.png)

Now, let us assume that environment label is not present in the `values.yaml` file. As we know, this field is optional.
Hence, it should be ignored when creating manifest file. To implement that logic, we are using if conditions.

`service.yaml`

```html

apiVersion: v1
kind: Service
metadata:
  name: {{ .Release.Name }}-service
  {{ if .Values.environment }}
  labels:
    environment: {{ .Values.environment }}
  {{ end }}
spec:
  type: {{ .Values.service.type }}
  selector:
    app.kubernetes.io/name: MyApp
  ports:
    - port: {{ .Values.service.port }}
      targetPort: {{ .Values.service.port }}
      nodePort: 30007
```

Now, let us try to dry run using template command and see the result.

![helm_39.png](../assets/helm_39.png)

As you see in the above snapshot, you don't find `label` field in the `service.yaml` manifest file because environment 
label is not present in the `values.yaml`.

However, if you notice closely the manifest file, you will be able to identify the empty line in the metadata section
where `labels` field comes. This is because helm expects a field, but it is not available and hence helm leaves the entire
line as empty. We can trim this empty line as well. To do so, we need to include "-" in the if conditional block.


`service.yaml`

```html

apiVersion: v1
kind: Service
metadata:
  name: {{ .Release.Name }}-service
  {{- if .Values.environment }}
  labels:
    environment: {{ .Values.environment }}
  {{- end }}
spec:
  type: {{ .Values.service.type }}
  selector:
    app.kubernetes.io/name: MyApp
  ports:
    - port: {{ .Values.service.port }}
      targetPort: {{ .Values.service.port }}
      nodePort: 30007
```

![helm_40.png](../assets/helm_40.png)

## Create Manifest Files Based On Conditions

In case, if you want to create the manifest file only if certain conditions are met. Else, you don't need to create them.
To do so, you have to update the entire YAML file in the if condition itself. Also add the required field in the `values.yaml`
file.

`service.yaml`

```html

{{- if .Values.required }}
apiVersion: v1
kind: Service
metadata:
  name: {{ .Release.Name }}-service
  {{- if .Values.environment }}
  labels:
    environment: {{ .Values.environment }}
  {{- end }}
spec:
  type: {{ .Values.service.type }}
  selector:
    app.kubernetes.io/name: MyApp
  ports:
    - port: {{ .Values.service.port }}
      targetPort: {{ .Values.service.port }}
      nodePort: 30007
{{- end }}
```
`Remember that if condition should not have compared conditions such as eq, gt, and lt etc.`

![helm_41.png](../assets/helm_41.png)

![helm_42.png](../assets/helm_42.png)

When you run the template command, you will be able to see service.yaml file because `required` value is set to `true` in 
the `values.yaml` file.

![helm_43.png](../assets/helm_43.png)

Let's change `required` value is as `false` and verify now.

![helm_44.png](../assets/helm_44.png)

When you run the template command, you will be not able to see service.yaml file because `required` value is set to `false` in 
the `values.yaml` file.

![helm_45.png](../assets/helm_45.png)

## Scope of the elements (using with statement)

By default, all the elements have root scope. It will start with `.` and then their absolute object path. We can reduce
to write the entire object path by using `with` statement.

Let us assume that `values.yaml` file have the following properties.

![helm_46.png](../assets/helm_46.png)

Update the `service.yaml` file.

`service.yaml`

```html
apiVersion: v1
kind: Service
metadata:
  name: {{ .Release.Name }}-service
  labels:
    environment: {{ .Values.environment }}
    {{- with .Values.web }}
    name: {{ .tier.name }}
    numberOfServers: {{ .tier.numberOfServers }}
    {{- end }}
    {{- with .Values.db }}
    name: {{ .tier.name }}
    numberOfServers: {{ .tier.numberOfServers }}
    {{- end }}    
spec:
  type: {{ .Values.service.type }}
  selector:
    app.kubernetes.io/name: MyApp
  ports:
    - port: {{ .Values.service.port }}
      targetPort: {{ .Values.service.port }}
      nodePort: 30007
```

![helm_47.png](../assets/helm_47.png)

When you run the template command, you will be able to see all the values. However, we didn't mention a full object path 
for all the label properties.

![helm_48.png](../assets/helm_48.png)

If we want to include the root scope element within `with` statement block, then we must use `$` in the properties.

`service.yaml`

```html
apiVersion: v1
kind: Service
metadata:
  name: {{ .Release.Name }}-service
  labels:
    environment: {{ .Values.environment }}
    {{- with .Values.web }}
    name: {{ .tier.name }}
    numberOfServers: {{ .tier.numberOfServers }}
    {{- end }}
    {{- with .Values.db }}
    name: {{ .tier.name }}
    numberOfServers: {{ .tier.numberOfServers }}
    release: {{ $.Release.Name }}
    {{- end }}    
spec:
  type: {{ .Values.service.type }}
  selector:
    app.kubernetes.io/name: MyApp
  ports:
    - port: {{ .Values.service.port }}
      targetPort: {{ .Values.service.port }}
      nodePort: 30007
```

![helm_49.png](../assets/helm_49.png)

## Using range statement

If the properties are too many, and you don't need to include one by one as it is a tedious job. Instead, you can use 
`range` statement.

### List of data updated in manifest file

`values.yaml`

![helm_50.png](../assets/helm_50.png)

`configmap.yaml`

![helm_51.png](../assets/helm_51.png)

### Dictionary of data updated in manifest file

`values.yaml`

![helm_46.png](../assets/helm_46.png)

`service.yaml`

```html
apiVersion: v1
kind: Service
metadata:
  name: {{ .Release.Name }}-service
  labels:
    environment: {{ .Values.environment }}
    {{- range $key, $value := $.Values.web.tier }}
    {{ $key }}: {{ $value }}
    {{- end }}
    {{- range $key, $value := $.Values.db.tier }}
    {{ $key }}: {{ $value }}
    release: {{ $.Release.Name }} 
    {{- end }}
spec:
  type: {{ .Values.service.type }}
  selector:
    app.kubernetes.io/name: MyApp
  ports:
    - port: {{ .Values.service.port }}
      targetPort: {{ .Values.service.port }}
      nodePort: 30007
```

![helm_52.png](../assets/helm_52.png)

When you run the template command, you will be able to see the below 

![helm_53.png](../assets/helm_53.png)

### Named Templates

Let us assume that there are labels which are repeated in multiple places and multiple manifest files.
So, updating them in all the places and all the manifest files are complex in nature. 
Instead, we update the labels in `_helpers.tpl` file and use them in the manifest files wherever required.

`NOTE: File name starts with '_' will be a template file and helm will not consider them as a normal kubernetes object files.
Hence, it will not be considered while creating k8s objects.`

`_helpers.tpl`

![helm_54.png](../assets/helm_54.png)

```html
{{- define "labels" }}
  app: nginx
  environment: prod
{{- end }}
```

Remember that indentation is important when you update the values in the `_helper.tpl` file because the same indentation
will be applied in the manifest files when created.

Let us implement the labels in the `service.yaml` file.

`service.yaml`

```html
apiVersion: v1
kind: Service
metadata:
  name: {{ .Release.Name }}-service
  labels:
    {{- template "labels" }}
spec:
  type: {{ .Values.service.type }}
  selector:
    app.kubernetes.io/name: MyApp
  ports:
    - port: {{ .Values.service.port }}
      targetPort: {{ .Values.service.port }}
      nodePort: 30007
```

![helm_55.png](../assets/helm_55.png)

Now, let us run the helm template command.

![helm_56.png](../assets/helm_56.png)

As you see the above snapshot, 
there are only two spaces indentations applied in the service.yaml as the `_helpers.tpl` file
has only two space indentations of those label values. 
Also, you cannot increase the indentation in the `_helpers.tpl` file as
those labels may be included in different places where different indentations are needed in those places.

To avoid this issue, we need to use `indent` function.
However, functions cannot be pipelined in `template` statement.
So, we must use `include` statement instead of `template` statement


`service.yaml`

```html
apiVersion: v1
kind: Service
metadata:
  name: {{ .Release.Name }}-service
  labels:
    {{- include "labels" . | indent 2}}
spec:
  type: {{ .Values.service.type }}
  selector:
    app.kubernetes.io/name: MyApp
  ports:
    - port: {{ .Values.service.port }}
      targetPort: {{ .Values.service.port }}
      nodePort: 30007
```

`Remember that you need to change the indent value wherever you applied. For example, if the labels are applied with 4 spaces
indentations, then in those places you need update indent 4`


![helm_57.png](../assets/helm_57.png)

Now, let us run the helm template command.

![helm_58.png](../assets/helm_58.png)




