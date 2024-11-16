# **Задание №1**
Спроектировать БД аналогичную структуре БД «Студент» из презентации (слайд № 34)
Проектируемая БД должна состоять минимум из 4-х связанных таблиц (уровень детализации должен быть сопоставим с БД «Cтудент» и в ней между сущностями должно быть отношение М:М.
Далее выполнить все задания (лабораторные) из примера контрольной работы и оформить их аналогично примеру для спроектированной Вами БД  
# **Ход выполнения**  
Для реализации проекта я использовал MySQL Workbench. Изначально была создана модель.
Формируем скрипт создания БД и заполняем таблицу данными:  

```sql
-- MySQL dump 10.13  Distrib 8.0.40, for Win64 (x86_64)
--
-- Host: 127.0.0.1    Database: labamodel
-- ------------------------------------------------------
-- Server version	9.1.0

/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!50503 SET NAMES utf8 */;
/*!40103 SET @OLD_TIME_ZONE=@@TIME_ZONE */;
/*!40103 SET TIME_ZONE='+00:00' */;
/*!40014 SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0 */;
/*!40014 SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0 */;
/*!40101 SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='NO_AUTO_VALUE_ON_ZERO' */;
/*!40111 SET @OLD_SQL_NOTES=@@SQL_NOTES, SQL_NOTES=0 */;

--
-- Table structure for table `изготовители`
--

DROP TABLE IF EXISTS `изготовители`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `изготовители` (
  `Код` int NOT NULL,
  `Наименование` varchar(45) DEFAULT NULL,
  `Страна` varchar(45) DEFAULT NULL,
  `Сайт` varchar(45) DEFAULT NULL,
  PRIMARY KEY (`Код`),
  CONSTRAINT `Код_изготовитля` FOREIGN KEY (`Код`) REFERENCES `прайс-лист` (`Код изготовителя`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb3;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `изготовители`
--

LOCK TABLES `изготовители` WRITE;
/*!40000 ALTER TABLE `изготовители` DISABLE KEYS */;
INSERT INTO `изготовители` VALUES (1,'Завод Audi','Германия','example.com'),(2,'Завод Toyota','Япония','example.com'),(3,'Завод Honda','Япония','example.com'),(4,'Завод BMW','Германия','example.com');
/*!40000 ALTER TABLE `изготовители` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `модели`
--

DROP TABLE IF EXISTS `модели`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `модели` (
  `Код` int NOT NULL,
  `Наименование` varchar(45) DEFAULT NULL,
  `Код изготовителя` int DEFAULT NULL,
  PRIMARY KEY (`Код`),
  UNIQUE KEY `Код изготовителя_UNIQUE` (`Код изготовителя`),
  CONSTRAINT `Код_изготовитля_` FOREIGN KEY (`Код изготовителя`) REFERENCES `изготовители` (`Код`),
  CONSTRAINT `Код_модели` FOREIGN KEY (`Код`) REFERENCES `прайс-лист` (`Код модели`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb3;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `модели`
--

LOCK TABLES `модели` WRITE;
/*!40000 ALTER TABLE `модели` DISABLE KEYS */;
INSERT INTO `модели` VALUES (1,'Audi',1),(2,'Toyota',2),(3,'Honda',3),(4,'BMW',4);
/*!40000 ALTER TABLE `модели` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `прайс-лист`
--

DROP TABLE IF EXISTS `прайс-лист`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `прайс-лист` (
  `Код записи` int NOT NULL,
  `Код продавца` int NOT NULL,
  `Код изготовителя` int NOT NULL,
  `Код товара` int NOT NULL,
  `Код модели` int NOT NULL,
  `Цена` decimal(10,0) NOT NULL,
  PRIMARY KEY (`Код записи`),
  UNIQUE KEY `Код продавца_UNIQUE` (`Код продавца`),
  UNIQUE KEY `Код изготовителя_UNIQUE` (`Код изготовителя`),
  UNIQUE KEY `Код товара_UNIQUE` (`Код товара`),
  UNIQUE KEY `Код модели_UNIQUE` (`Код модели`),
  UNIQUE KEY `Цена_UNIQUE` (`Цена`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb3;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `прайс-лист`
--

LOCK TABLES `прайс-лист` WRITE;
/*!40000 ALTER TABLE `прайс-лист` DISABLE KEYS */;
INSERT INTO `прайс-лист` VALUES (1,1,1,1,1,100),(2,2,2,2,2,200),(3,3,3,3,3,300),(4,4,4,4,4,400);
/*!40000 ALTER TABLE `прайс-лист` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `продавцы`
--

DROP TABLE IF EXISTS `продавцы`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `продавцы` (
  `Код` int NOT NULL,
  `ФИО` varchar(45) NOT NULL,
  `Адрес` varchar(45) DEFAULT NULL,
  `Номер телефона` varchar(45) DEFAULT NULL,
  `Сайт` varchar(45) DEFAULT NULL,
  PRIMARY KEY (`Код`),
  CONSTRAINT `Код` FOREIGN KEY (`Код`) REFERENCES `прайс-лист` (`Код продавца`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb3;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `продавцы`
--

LOCK TABLES `продавцы` WRITE;
/*!40000 ALTER TABLE `продавцы` DISABLE KEYS */;
INSERT INTO `продавцы` VALUES (1,'Иванов Иван Иванович','Москва','8 999 999 99 99','example.com'),(2,'Петров Петр Петрович','Самара','8 999 999 99 98','example.com'),(3,'Игорев Игорь Игоревич','Екатеринбург','8 999 999 99 97','example.com'),(4,'Родионова Мария Ивановна','Санкт-Петербург','8 999 999 99 96','example.com');
/*!40000 ALTER TABLE `продавцы` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `товары`
--

DROP TABLE IF EXISTS `товары`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `товары` (
  `Код` int NOT NULL,
  `наименование` varchar(45) DEFAULT NULL,
  PRIMARY KEY (`Код`),
  CONSTRAINT `Код товара` FOREIGN KEY (`Код`) REFERENCES `прайс-лист` (`Код товара`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb3;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `товары`
--

LOCK TABLES `товары` WRITE;
/*!40000 ALTER TABLE `товары` DISABLE KEYS */;
INSERT INTO `товары` VALUES (1,'Комплектация А'),(2,'Комплектация Б'),(3,'Комплектация В'),(4,'Комплектация Г');
/*!40000 ALTER TABLE `товары` ENABLE KEYS */;
UNLOCK TABLES;
/*!40103 SET TIME_ZONE=@OLD_TIME_ZONE */;

/*!40101 SET SQL_MODE=@OLD_SQL_MODE */;
/*!40014 SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS */;
/*!40014 SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS */;
/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
/*!40111 SET SQL_NOTES=@OLD_SQL_NOTES */;

-- Dump completed on 2024-11-16 18:44:30
```
