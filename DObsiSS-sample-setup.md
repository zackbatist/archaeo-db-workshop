CREATE DATABASE DObsiSS;
CREATE USER 'zack'@'localhost' IDENTIFIED BY 'batist';
CREATE USER 'zack'@'12.34.56.78' IDENTIFIED BY 'batist';
GRANT ALL PRIVILEGES ON DObsiSS.* TO 'zack'@'%' IDENTIFIED BY 'batist';
FLUSH PRIVILEGES;
mysql -u zack -p

CREATE TABLE `DObsiSS`.`sites` (
`id` INT(11) UNSIGNED NOT NULL AUTO_INCREMENT,
`site` VARCHAR(255) DEFAULT '',
`lat` VARCHAR(255) DEFAULT '',
`lon` VARCHAR(255) DEFAULT '',
`country` VARCHAR(255) DEFAULT '',
`retired` BIT DEFAULT '',
PRIMARY KEY (`id`)
);

INSERT INTO `DObsiSS`.`sites` (site, lat, lon, country, retired) VALUES ("Toronto", "43.7001100", "-79.4163000", "Canada", 0);
SELECT `site`, `lat`, `lon` FROM `sites` WHERE `sites`.`site` = "Toronto";
UPDATE `DSbsiSS`.`sites` SET `retired` = "1" WHERE `site` = "Toronto";
DELETE FROM `sites` WHERE `site` = "Toronto";

CREATE TABLE `DObsiSS`.`datapoints` (
`id` INT(11) SIGNED NOT NULL AUTO_INCREMENT,
`slice` VARCHAR(255) DEFAULT '',
`site` VARCHAR(255) DEFAULT '',
`diagnosticfeatures` VARCHAR(255) DEFAULT '',
PRIMARY KEY (`id`)
);

INSERT INTO `DObsiSS`.`sites` (site, lat, lon, country, retired)
VALUES ("Toronto", "43.7001100", "-79.4163000", "Canada", 0);

INSERT INTO `DObsiSS`.`datapoints` (slice, site, diagnosticfeatures)
VALUES ("GreatestGen", "Toronto", "Horses and buggies, doilies");

INSERT INTO `DObsiSS`.`datapoints` (slice, site, diagnosticfeatures)
VALUES ("Boomers", "Toronto", "Vinyl records, blue jeans");

INSERT INTO `DObsiSS`.`datapoints` (slice, site, diagnosticfeatures)
VALUES ("GenX", "Toronto", "Walkman");

INSERT INTO `DObsiSS`.`datapoints` (slice, site, diagnosticfeatures)
VALUES ("Millenials", "Toronto", "Beanie babies, iPods");

INSERT INTO `DObsiSS`.`datapoints` (slice, site, diagnosticfeatures)
VALUES ("GenZ", "Toronto", "Fidget spinners, bad things");

INSERT INTO `DObsiSS`.`datapoints` (slice, site, diagnosticfeatures)
VALUES ("ApocalypseSurvivors", "Toronto", "sticks and stones");

ALTER TABLE `DObsiSS`.`datapoints`
ADD CONSTRAINT `FK-datapoints-site`
FOREIGN KEY (`site`)
REFERENCES `DObsiSS`.`sites` (`site`)
ON DELETE CASCADE ON UPDATE CASCADE;

SELECT `datapoints`.slice, `datapoints`.`diagnosticfeatures`, `sites`.`lat`, `sites`.lon`
FROM `datapoints` INNER JOIN `sites`
ON `sites`.`site` = `datapoints`.`site`;


