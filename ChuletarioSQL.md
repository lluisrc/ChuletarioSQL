## DATABASE
CREATE

## Operaciones CRUD

### Create


USE moviemapp_test;

CREATE TABLE `municipios` (
  `municipio` varchar(255) NOT NULL,
  `provincia_provincias` varchar(225) DEFAULT NULL,
  PRIMARY KEY (`municipio`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

INSERT INTO `municipios` VALUES ('Alegria-Dulantzi','Alava'),('Amurrio','Alava'),('Anana','Alava')...


ALTER TABLE municipios DROP PRIMARY KEY, ADD id INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY;

ALTER TABLE municipios modify column municipio varchar(255) after id;

UPDATE municipios
SET id_provincias = 52
WHERE provincia_provincias = 'Zaragoza';

commit;
SELECT * FROM provincias;


USE moviemapp_test;

ALTER TABLE provincias MODIFY id_comunidades_autonomas INT NOT NULL;

CREATE TABLE `municipios` (
  `municipio` varchar(255) NOT NULL,
  `provincia_provincias` varchar(225) DEFAULT NULL,
  PRIMARY KEY (`municipio`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;


ALTER TABLE comunidades_autonomas MODIFY id INT NOT NULL;

ALTER TABLE municipios DROP PRIMARY KEY, ADD id INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY;

SELECT * FROM municipios;

ALTER TABLE municipios modify column municipio varchar(255) after id;

UPDATE municipios
SET id_provincias = 52
WHERE provincia_provincias = 'Zaragoza';

commit;
SELECT * FROM comunidades_autonomas;


ALTER TABLE provincias ADD FOREIGN KEY (id_comunidades_autonomas) REFERENCES comunidades_autonomas(id);
ALTER TABLE municipios ADD FOREIGN KEY (id_provincias) REFERENCES provincias(id);
