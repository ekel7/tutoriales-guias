# Tutoriales-guias - PowerCRM SQ3
  Este repo se hizo para ir registrando posibles problemas y soluciones para el backend de PowerCRM.

## Posibles problemas

### __Microservicio no se puede conectar a otro una vez subido a openshift(puede ser que funcione en un ambiente pero en otro se rompa) - 31/08/2022__

#### Solución posible:
    Chequear que esten bien las rutas de cada ambiente en los archivos de la carpeta overlays, seguir las siguientes plantillas para los diferentes ambientes:


### CERT / PROD (para prod solo se quita la palabra cert)

Un error comun acá seria que no le pasamos el punto despues del nombre del MS, o sea cuando termina el nombre del ms deberia haber un punto y luego el ambiente, así; __movistar-fcd-calculator-bonification.movistar-cert-powercrm__.
```yaml
configMapGenerator:
  - name: movistar-fcd-calculator-bonification
    literals:
      - PORT=8080
      - PRODUCT_OFFERING_SERVER=http://movistar-prod-offering-int.movistar-cert-powercrm.apps.ocpnp.cuyorh.tcloud.ar
      - PRODUCT_OFFERING_PATH=/movistar-prod-offering-int/v1/phone-numbers/{phone_number}/product-offer
      - PRODUCT_OFFERING_DATA_PATH=/movistar-prod-offering-int/v1/product-offer/{offer_id}
      - STDOUT_LOGS=off
      - ELK_LOGS=on
      - ELK_LOGS_DEBUG=off
```

### INT / DEV

```yaml
configMapGenerator:
  - name: movistar-fcd-calculator-bonification
    literals:
      - PORT=8080
      - PRODUCT_OFFERING_SERVER=http://movistar-prod-offering-int-movistar-int-powercrm.apps.ocpnp.cuyorh.tcloud.ar
      - PRODUCT_OFFERING_PATH=/movistar-prod-offering-int/v1/phone-numbers/{phone_number}/product-offer
      - PRODUCT_OFFERING_DATA_PATH=/movistar-prod-offering-int/v1/product-offer/{offer_id}
      - STDOUT_LOGS=on
      - ELK_LOGS=on
      - ELK_LOGS_DEBUG=off
```

