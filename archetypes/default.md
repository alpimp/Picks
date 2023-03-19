---
title: "{{ replace ( replace .Name "-" " ") "_" "/" | title }}"
date: {{ .Date }}
{{- if and (getenv "KEYS") (getenv "VALUES") }}
  {{- $keys := split (getenv "KEYS" ) "|" }}
  {{- $values := split (getenv "VALUES") "|" }}
  {{- if ne (len $keys) (len $values) }}
    {{- errorf "The number of VALUES must match the number of KEYS."}}
  {{- end }}
  {{- range $k, $v := $keys }}
{{ $v }}  {{ index $values $k }}
  {{- end }}
{{- end }}
---

