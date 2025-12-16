## Lab 8 : Sauvegarde, restauration et optimisation


## Script SQL :
```sql
-- MariaDB dump 10.19  Distrib 10.4.32-MariaDB, for Win64 (AMD64)
--
-- Host: localhost    Database: universite_test
-- ------------------------------------------------------
-- Server version	10.4.32-MariaDB

/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8mb4 */;
/*!40103 SET @OLD_TIME_ZONE=@@TIME_ZONE */;
/*!40103 SET TIME_ZONE='+00:00' */;
/*!40014 SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0 */;
/*!40014 SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0 */;
/*!40101 SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='NO_AUTO_VALUE_ON_ZERO' */;
/*!40111 SET @OLD_SQL_NOTES=@@SQL_NOTES, SQL_NOTES=0 */;

--
-- Table structure for table `cours`
--

DROP TABLE IF EXISTS `cours`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `cours` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `titre` varchar(200) NOT NULL,
  `code` varchar(20) NOT NULL,
  `credits` int(11) NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `code` (`code`)
) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `cours`
--

LOCK TABLES `cours` WRITE;
/*!40000 ALTER TABLE `cours` DISABLE KEYS */;
INSERT INTO `cours` VALUES (1,'Programmation Java','CS101',4),(2,'Algèbre Linéaire','MA201',3),(3,'Bases de Données','CS102',4);
/*!40000 ALTER TABLE `cours` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `enseignement`
--

DROP TABLE IF EXISTS `enseignement`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `enseignement` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `cours_id` int(11) NOT NULL,
  `professeur_id` int(11) DEFAULT NULL,
  `semestre` varchar(20) NOT NULL,
  PRIMARY KEY (`id`),
  KEY `fk_ens_cours` (`cours_id`),
  KEY `fk_ens_prof` (`professeur_id`),
  CONSTRAINT `fk_ens_cours` FOREIGN KEY (`cours_id`) REFERENCES `cours` (`id`),
  CONSTRAINT `fk_ens_prof` FOREIGN KEY (`professeur_id`) REFERENCES `professeur` (`id`) ON DELETE SET NULL
) ENGINE=InnoDB AUTO_INCREMENT=3 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `enseignement`
--

LOCK TABLES `enseignement` WRITE;
/*!40000 ALTER TABLE `enseignement` DISABLE KEYS */;
INSERT INTO `enseignement` VALUES (1,1,1,'S1'),(2,2,2,'S1');
/*!40000 ALTER TABLE `enseignement` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `etudiant`
--

DROP TABLE IF EXISTS `etudiant`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `etudiant` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `nom` varchar(100) NOT NULL,
  `email` varchar(150) NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `email` (`email`)
) ENGINE=InnoDB AUTO_INCREMENT=3 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `etudiant`
--

LOCK TABLES `etudiant` WRITE;
/*!40000 ALTER TABLE `etudiant` DISABLE KEYS */;
INSERT INTO `etudiant` VALUES (1,'Alice','alice@mail.com'),(2,'Bob','bob@mail.com');
/*!40000 ALTER TABLE `etudiant` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `etudiant_csv`
--

DROP TABLE IF EXISTS `etudiant_csv`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `etudiant_csv` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `nom` varchar(100) NOT NULL,
  `email` varchar(150) NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `email` (`email`)
) ENGINE=InnoDB AUTO_INCREMENT=3 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `etudiant_csv`
--

LOCK TABLES `etudiant_csv` WRITE;
/*!40000 ALTER TABLE `etudiant_csv` DISABLE KEYS */;
INSERT INTO `etudiant_csv` VALUES (1,'Alice','alice@mail.com'),(2,'Bob','bob@mail.com');
/*!40000 ALTER TABLE `etudiant_csv` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `examen`
--

DROP TABLE IF EXISTS `examen`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `examen` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `inscription_id` int(11) NOT NULL,
  `date_examen` date NOT NULL,
  `score` decimal(4,2) NOT NULL,
  PRIMARY KEY (`id`),
  KEY `fk_exam_ins` (`inscription_id`),
  CONSTRAINT `fk_exam_ins` FOREIGN KEY (`inscription_id`) REFERENCES `inscription` (`id`),
  CONSTRAINT `ck_score` CHECK (`score` between 0 and 20)
) ENGINE=InnoDB AUTO_INCREMENT=5 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `examen`
--

LOCK TABLES `examen` WRITE;
/*!40000 ALTER TABLE `examen` DISABLE KEYS */;
INSERT INTO `examen` VALUES (1,1,'2025-12-16',15.50),(2,2,'2025-12-16',12.00),(3,3,'2025-12-16',18.00),(4,4,'2025-12-16',14.50);
/*!40000 ALTER TABLE `examen` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `inscription`
--

DROP TABLE IF EXISTS `inscription`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `inscription` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `etudiant_id` int(11) NOT NULL,
  `enseignement_id` int(11) NOT NULL,
  `date_inscription` date NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `etudiant_id` (`etudiant_id`,`enseignement_id`),
  KEY `fk_ins_enseignement` (`enseignement_id`),
  CONSTRAINT `fk_ins_enseignement` FOREIGN KEY (`enseignement_id`) REFERENCES `enseignement` (`id`),
  CONSTRAINT `fk_ins_etudiant` FOREIGN KEY (`etudiant_id`) REFERENCES `etudiant` (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=5 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `inscription`
--

LOCK TABLES `inscription` WRITE;
/*!40000 ALTER TABLE `inscription` DISABLE KEYS */;
INSERT INTO `inscription` VALUES (1,1,1,'2025-12-16'),(2,2,1,'2025-12-16'),(3,1,2,'2025-12-16'),(4,2,2,'2025-12-16');
/*!40000 ALTER TABLE `inscription` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `professeur`
--

DROP TABLE IF EXISTS `professeur`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `professeur` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `nom` varchar(100) NOT NULL,
  `email` varchar(150) NOT NULL,
  `departement` varchar(100) NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `email` (`email`)
) ENGINE=InnoDB AUTO_INCREMENT=3 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `professeur`
--

LOCK TABLES `professeur` WRITE;
/*!40000 ALTER TABLE `professeur` DISABLE KEYS */;
INSERT INTO `professeur` VALUES (1,'Dr. Martin','martin@uni.edu','Informatique'),(2,'Dr. Durand','durand@uni.edu','Mathématiques');
/*!40000 ALTER TABLE `professeur` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Temporary table structure for view `vue_etudiant_charges`
--

DROP TABLE IF EXISTS `vue_etudiant_charges`;
/*!50001 DROP VIEW IF EXISTS `vue_etudiant_charges`*/;
SET @saved_cs_client     = @@character_set_client;
SET character_set_client = utf8;
/*!50001 CREATE VIEW `vue_etudiant_charges` AS SELECT
 1 AS `etudiant_id`,
  1 AS `etudiant`,
  1 AS `nb_inscriptions`,
  1 AS `total_credits` */;
SET character_set_client = @saved_cs_client;

--
-- Temporary table structure for view `vue_performances`
--

DROP TABLE IF EXISTS `vue_performances`;
/*!50001 DROP VIEW IF EXISTS `vue_performances`*/;
SET @saved_cs_client     = @@character_set_client;
SET character_set_client = utf8;
/*!50001 CREATE VIEW `vue_performances` AS SELECT
 1 AS `etudiant_id`,
  1 AS `nom`,
  1 AS `moyenne_score` */;
SET character_set_client = @saved_cs_client;

--
-- Dumping events for database 'universite_test'
--

--
-- Dumping routines for database 'universite_test'
--

--
-- Final view structure for view `vue_etudiant_charges`
--

/*!50001 DROP VIEW IF EXISTS `vue_etudiant_charges`*/;
/*!50001 SET @saved_cs_client          = @@character_set_client */;
/*!50001 SET @saved_cs_results         = @@character_set_results */;
/*!50001 SET @saved_col_connection     = @@collation_connection */;
/*!50001 SET character_set_client      = cp850 */;
/*!50001 SET character_set_results     = cp850 */;
/*!50001 SET collation_connection      = cp850_general_ci */;
/*!50001 CREATE ALGORITHM=UNDEFINED */
/*!50013 DEFINER=`root`@`localhost` SQL SECURITY DEFINER */
/*!50001 VIEW `vue_etudiant_charges` AS select `et`.`id` AS `etudiant_id`,`et`.`nom` AS `etudiant`,count(`i`.`id`) AS `nb_inscriptions`,sum(`c`.`credits`) AS `total_credits` from (((`etudiant` `et` join `inscription` `i` on(`et`.`id` = `i`.`etudiant_id`)) join `enseignement` `ens` on(`i`.`enseignement_id` = `ens`.`id`)) join `cours` `c` on(`ens`.`cours_id` = `c`.`id`)) group by `et`.`id`,`et`.`nom` */;
/*!50001 SET character_set_client      = @saved_cs_client */;
/*!50001 SET character_set_results     = @saved_cs_results */;
/*!50001 SET collation_connection      = @saved_col_connection */;

--
-- Final view structure for view `vue_performances`
--

/*!50001 DROP VIEW IF EXISTS `vue_performances`*/;
/*!50001 SET @saved_cs_client          = @@character_set_client */;
/*!50001 SET @saved_cs_results         = @@character_set_results */;
/*!50001 SET @saved_col_connection     = @@collation_connection */;
/*!50001 SET character_set_client      = cp850 */;
/*!50001 SET character_set_results     = cp850 */;
/*!50001 SET collation_connection      = cp850_general_ci */;
/*!50001 CREATE ALGORITHM=UNDEFINED */
/*!50013 DEFINER=`root`@`localhost` SQL SECURITY DEFINER */
/*!50001 VIEW `vue_performances` AS select `et`.`id` AS `etudiant_id`,`et`.`nom` AS `nom`,avg(`e`.`score`) AS `moyenne_score` from ((`etudiant` `et` left join `inscription` `i` on(`et`.`id` = `i`.`etudiant_id`)) left join `examen` `e` on(`i`.`id` = `e`.`inscription_id`)) group by `et`.`id`,`et`.`nom` */;
/*!50001 SET character_set_client      = @saved_cs_client */;
/*!50001 SET character_set_results     = @saved_cs_results */;
/*!50001 SET collation_connection      = @saved_col_connection */;
/*!40103 SET TIME_ZONE=@OLD_TIME_ZONE */;

/*!40101 SET SQL_MODE=@OLD_SQL_MODE */;
/*!40014 SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS */;
/*!40014 SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS */;
/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
/*!40111 SET SQL_NOTES=@OLD_SQL_NOTES */;

-- Dump completed on 2025-12-16 19:42:14
```
## capture d'ecran :

![image alt](https://github.com/laouysalma/Tp8MySQL/blob/main/Ex1.jpg?raw=true)

![image alt](https://github.com/laouysalma/Tp8MySQL/blob/main/Ex2.jpg?raw=true)
