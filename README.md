# CyberDB 

Group 11 Team Project - CS 3743-004 Fall 2023 UTSA

Description: A forensic database that has data on iot devices that can be used to gather information within an investigation. The goal of this database is to provide information and cooperation between forensic scientists,
investigators, agencies, and organizations that can use this database for the sake of public safety.

-- Create a database
CREATE DATABASE CyberDB;

-- Use the database
USE CyberDB;

-- Create a table 'Data Entry'
CREATE TABLE DataEntry (
  DataEntry_ID INT PRIMARY KEY,
  DataEntry_Notes VARCHAR(50) NOT NULL,
  DataEntryExtractedDataFiles VARCHAR(200) NOT NULL,
  FOREIGN KEY (Device_ID) REFERENCES Device(Device_ID),
  FOREIGN KEY (Tool_ID) REFERENCES Tool(Tool_ID)
);

-- Create a table 'Device'
CREATE TABLE Device (
  Device_ID INT PRIMARY KEY,
  Device_Type VARCHAR(50) NOT NULL,
  Device_PhysicalStateDescript VARCHAR(100) NOT NULL,
  Device_HardwareSpecs VARCHAR(100) NOT NULL,
  FOREIGN KEY (Investigator_ID) REFERENCES Investigator(Investigator_ID)
);

-- Create a table 'InvestigativeAction'
CREATE TABLE InvestigativeAction (
  InvestigativeAction_ID INT PRIMARY KEY,
  InvestigativeAction_Description VARCHAR(200) NOT NULL,
  InestigativeAction_TimeStamp TIMESTAMP(),
  FOREIGN KEY (Device_ID) REFERENCES Device(Device_ID)
);
-- Create a table 'Tool'
CREATE TABLE Tool (
  Tool_ID INT PRIMARY KEY,
  Tool_Name VARCHAR(50) NOT NULL
);
-- Create a table 'Investigator'
CREATE TABLE Investigator (
  Investigator_ID INT PRIMARY KEY,
  Investigatator_FirstName VARCHAR(50) NOT NULL,
  Investigator_LastName VARCHAR(50) NOT NULL
);
-- Create a table 'ChainOfCustodyRecord'
CREATE TABLE ChainOfCustodyRecord (
  ChainOfCustodyRecord_ID INT PRIMARY KEY,
  ChainOfCustodyRecord_TimeStamp TIMESTAMP(),
  FOREIGN KEY (Investigator_ID) REFERENCES Investigator(Investigator_ID),
  FOREIGN KEY (Device_ID) REFERENCES Device(Device_ID)
);
-- Create a table 'DisassemblyRecord'
CREATE TABLE DisassemblyRecord (
  Disassembly_ID INT PRIMARY KEY,
  Disassembly_Description VARCHAR(200) NOT NULL,
  Disassembly_Timestamp TIMESTAMP(),
  FOREIGN KEY (InvestigativeAction_ID) REFERENCES InvestigativeAction(InvestigativeAction_ID),
  FOREIGN KEY (Device_ID) REFERENCES Device(Device_ID)
);
