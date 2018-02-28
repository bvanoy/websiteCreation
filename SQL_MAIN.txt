USE master
GO

IF EXISTS (SELECT * FROM sysdatabases
			WHERE name = 'RpgFandom')
	DROP DATABASE RpgFandom
	GO
	
USE master
GO
	
CREATE DATABASE RpgFandom
ON PRIMARY (NAME = RpgFandom_Data1,
	FILENAME = 'C:\SQL\RpgFandom_Data1.MDF',
	SIZE = 250MB,
	MAXSIZE = 400MB,
	FILEGROWTH = 0)
	
LOG ON (NAME = RpgFandom_LOG,
	FILENAME = 'C:\SQL\RpgFandom_Log.LDF',
	SIZE = 75MB,
	MAXSIZE = 100MB,
	FILEGROWTH = 0)
GO

	USE RpgFandom
	GO

	IF EXISTS (SELECT * FROM sysobjects
				WHERE name = 'BuildSourcesTbl')
		DROP PROC BuildSourcesTbl
		GO

	CREATE PROC BuildSourcesTbl
	AS
	BEGIN
		IF EXISTS (SELECT * FROM sysobjects
					WHERE name = 'Sources')
		DROP TABLE Sources
		
		CREATE TABLE Sources
		(
			[Source Name] varchar(50),
			[Source Location] varchar(50)
		)
	END
	GO

	EXEC BuildSourcesTbl
	GO

	IF EXISTS (SELECT * FROM sysobjects
				WHERE name = 'PopulateSourcesTbl')
		DROP PROC PopulateSourcesTbl
		GO

	CREATE PROC PopulateSourcesTbl
	AS
	BEGIN
		DELETE Sources
		
		INSERT INTO Sources
		VALUES
		('Metacritic', 'http://www.metacritic.com/game'),
		('Google Images', 'https://www.google.com/imghp?hl=en&tab=wi'),
		('GameStop', 'http://www.gamestop.com/'),
		('GAMESPOT', 'http://www.gamespot.com/'),
		('Zelda Wiki', 'http://zeldawiki.org/The_Legend_of_Zelda_(Game)')
	END
	GO

	EXEC PopulateSourcesTbl
	GO

	IF EXISTS (SELECT * FROM sysobjects
				WHERE name = 'BuildContactInfoTbl')
		DROP PROC BuildContactInfoTbl
		GO

	CREATE PROC BuildContactInfoTbl
	AS
	BEGIN
		IF EXISTS (SELECT * FROM sysobjects
					WHERE name = 'ContactInfo')
		DROP TABLE ContactInfo
		
		CREATE TABLE ContactInfo
		(
			[Emailed To] varchar(50) DEFAULT 'brian.d.vanoy@gmail.com',
			[Emailed From] varchar(50),
			[Subject] varchar(20),
			[Message Summary] varchar(50),
			[Date Recieved] date
		)
	END
	GO

	EXEC BuildContactInfoTbl
	GO

	IF EXISTS (SELECT * FROM sysobjects
				WHERE name = 'PopulateContactInfoTbl')
		DROP PROC PopulateContactInfoTbl
		GO

	CREATE PROC PopulateContactInfoTbl
	AS
	BEGIN
		DELETE ContactInfo
		
		INSERT INTO ContactInfo
		VALUES
		(
			Default, 'brian.d.vanoy@gmail.com', 'Hello', 'Test Verification', GETDATE()
		)
	END
	GO

	EXEC PopulateContactInfoTbl
	GO

	IF EXISTS (SELECT * FROM sysobjects
				WHERE name = 'BuildGameReviewSitesTbl')
		DROP PROC BuildGameReviewSitesTbl
		GO

	CREATE PROC BuildGameReviewSitesTbl
	AS
	BEGIN
		IF EXISTS (SELECT * FROM sysobjects
					WHERE name = 'GameReviewSites')
		DROP TABLE GameReviewSites
		
		CREATE TABLE GameReviewSites
		(
			[Site Name] varchar(50),
			[Site Location] varchar(50)
		)
	END
	GO

	EXEC BuildGameReviewSitesTbl
	GO

	IF EXISTS (SELECT * FROM sysobjects
				WHERE name = 'PopulateGameReviewSitesTbl')
		DROP PROC PopulateGameReviewSitesTbl
		GO

	CREATE PROC PopulateGameReviewSitesTbl
	AS
	BEGIN
		DELETE GameReviewSites
		
		INSERT INTO GameReviewSites
		VALUES
		('IGN Reviews', 'http://www.ign.com/'),
		('GameStop', 'http://www.gamestop.com/'),
		('GAMESPOT', 'http://www.gamespot.com/'),
		('Metacritic', 'http://www.metacritic.com/game'),
		('Game Informer', 'http://www.gameinformer.com/reviews.aspx')
	END
	GO

	EXEC PopulateGameReviewSitesTbl
	GO

	IF EXISTS (SELECT * FROM sysobjects
				WHERE name = 'BuildFullGameListTbl')
		DROP PROC BuildFullGameListTbl
		GO

	CREATE PROC BuildFullGameListTbl
	AS
	BEGIN
		IF EXISTS (SELECT * FROM sysobjects
					WHERE name = 'FullGameList')
		DROP TABLE FullGameList
		
		CREATE TABLE FullGameList
		(
			[Game Name] varchar(50),
			[System Platform] varchar(50),
			[Release Date] date,
			[Metacritic Score] varchar(4),
			[Entry Date] date
		)
	END
	GO

	EXEC BuildFullGameListTbl
	GO

	IF EXISTS (SELECT * FROM sysobjects
				WHERE name = 'PopulateFullGameListTbl')
		DROP PROC PopulateFullGameListTbl
		GO

	CREATE PROC PopulateFullGameListTbl
	AS
	BEGIN
		DELETE FullGameList
		
		INSERT INTO FullGameList
		VALUES
		('Baten Kaitos: Eternal Wings And The Lost Ocean', 'GameCube', '11-16-2004', '86%', GETDATE()),
		('Baten Kaitos: Origins', 'GameCube', '09-25-2006', '75%', GETDATE()),
		('Bioshock', 'PS3/ 360/ PC', '08-01-2007', '96%', GETDATE()),
		('Bioshock 2', 'PS3/ 360/ PC', '02-09-2010', '88%', GETDATE()),
		('Body Harvest', 'N64', '09-30-1998', '73%', GETDATE()),
		('Borderlands', 'PS3/ 360/ PC', '10-20-2009', '83%', GETDATE()),
		('Brutal Legend', 'PS3/ 360', '10-13-2009', '83%', GETDATE()),
		('Chrono Trigger', 'SNES', '06-01-1995', '92%', GETDATE()),
		('Chrono Cross', 'PlayStation', '06-15-2000', '94%', GETDATE()),
		('Dark Cloud', 'PlayStation 2', '05-28-2001', '80%', GETDATE()),
		('Dark Cloud 2', 'PlayStation 2', '02-17-2003', '87%', GETDATE()),
		('Darksiders', 'PS3/ 360/ PC', '01-05-2010', '83%', GETDATE()),
		('Demon''s Souls', 'PlayStation 3', '10-06-2009', '89%', GETDATE()),
		('Dark Souls', 'PS3/ 360/ PC', '10-04-2011', '89%', GETDATE()),
		('Dead Space', 'PS3/ 360/ PC', '10-13-2008', '89%', GETDATE()),
		('Dead Space 2', 'PS3/ 360/ PC', '01-25-11', '89%', GETDATE()),
		('Dragon Age: Origins', 'PS3/ 360/ PC', '11-03-2009', '88%', GETDATE()),
		('Dragon Age 2', 'PS3/ 360/ PC', '03-08-2011', '81%', GETDATE()),
		('Elder Scrolls IV: Oblivion', 'PS3/ 360/ PC', '03-20-2006', '94%', GETDATE()),
		('Elder Scrolls V: Skyrim', 'PS3/ 360/ PC', '11-11-2011', '94%', GETDATE()),
		('Fallout 3', 'PS3/ 360/ PC', '10-28-2008', '91%', GETDATE()),
		('Fallout: New Vegas', 'PS3/ 360/ PC', '10-19-2010', '83%', GETDATE()),
		('Final Fantasy', 'NES', '12-18-1987', '80%', GETDATE()),
		('Final Fantasy II', 'SNES', '12-17-1988', '80%', GETDATE()),
		('Final Fantasy III', 'SNES', '04-27-1990', '77%', GETDATE()),
		('Final Fantasy IV', 'SNES', '12-01-1991', '85%', GETDATE()),
		('Final Fantasy V', 'SNES', '12-01-1992', '83%', GETDATE()),
		('Final Fantasy VI', 'SNES', '12-01-1994', '92%', GETDATE()),
		('Final Fantasy VII', 'PlayStation', '09-03-1997', '92%', GETDATE()),
		('Final Fantasy VIII', 'PlayStation', '09-07-1999', '90%', GETDATE()),
		('Final Fantasy IX', 'PlayStation', '11-13-2000', '94%', GETDATE()),
		('Final Fantasy X', 'PlayStation 2', '12-17-2001', '92%', GETDATE()),
		('Heavy Rain', 'PlayStation 3', '02-23-2010', '87%', GETDATE()),
		('The Legend Of Dragoon', 'PlayStation', '06-11-2000', '74%', GETDATE()),
		('Legend Of Zelda', 'NES', '09-27-1987', '84%', GETDATE()),
		('Zelda II: The Adventure Of Link', 'NES', '12-01-1988', '73%', GETDATE()),
		('Legend Of Zelda: A Link To The Past', 'SNES', '04-13-1992', '95%', GETDATE()),
		('Legend Of Zelda: Link''s Awakening DX', 'GB Color', '08-01-1998', '87%', GETDATE()),
		('Legend Of Zelda: Ocarina Of Time', 'N64', '11-23-1998', '99%', GETDATE()),
		('Legend Of Zelda: Majora''s Mask', 'N64', '10-25-2000', '95%', GETDATE()),
		('Legend Of Zelda: Oracle Of Ages', 'GB Color', '03-14-2001', '92%', GETDATE()),
		('Legend Of Zelda: Oracle Of Seasons', 'GB Color', '03-14-2001', '92%', GETDATE()),
		('Legend Of Zelda: Four Swords', 'GB Advance', '12-02-2002', '81%', GETDATE()),
		('Legend Of Zelda: Wind Waker', 'GameCube', '03-24-2003', '96%', GETDATE()),
		('Legend Of Zelda: Four Swords Adventure', 'GameCube', '06-07-2004', '86%', GETDATE()),
		('Legend Of Zelda: The Minish Cap', 'GB Advance', '01-10-2005', '89%', GETDATE()),
		('Legend Of Zelda: Twilight Princess', 'Nintendo Wii', '11-19-2006', '96%', GETDATE()),
		('Legend Of Zelda: Phantom Hourglass', 'Nintendo DS', '10-01-2007', '90%', GETDATE()),
		('Legend Of Zelda: Spirit Tracks', 'Nintendo DS', '12-07-2009', '87%', GETDATE()),
		('Legend Of Zelda: Skyward Sword', 'Nintendo Wii', '11-20-2011', '93%', GETDATE()),
		('Mario & Luigi: Superstar Saga', 'GB Advance', '11-17-2003', '90%', GETDATE()),
		('Mario & Luigi: Partners In Time', 'Nintendo DS', '11-28-2005', '86%', GETDATE()),
		('Mario & Luigi: Bowsers Inside Story', 'Nintendo DS', '09-14-2009', '90%', GETDATE()),
		('Mass Effect', 'Xbox/ PC', '11-20-2007', '91%', GETDATE()),
		('Mass Effect 2', 'PS3/ 360/ PC', '01-26-2011', '95%', GETDATE()),
		('Mass Effect 3', 'PS3/ 360/ PC', '03-06-2012', '92%', GETDATE()),
		('Metal Gear Solid', 'PlayStation', '10-21-1998', '94%', GETDATE()),
		('Metal Gear Solid 2: Sons Of Liberty', 'PlayStation 2', '11-12-2001', '96%', GETDATE()),
		('Metal Gear Solid 3: Snake Eater', 'PlayStation 2', '11-17-2004', '91%', GETDATE()),
		('Metal Gear Solid 4: Guns Of The Patriots', 'PlayStation 3', '06-12-2008', '94%', GETDATE()),
		('Metroid Prime', 'GameCube', '11-17-2002', '97%', GETDATE()),
		('Metroid Prime 2: Echoes', 'GameCube', '11-15-2004', '92%', GETDATE()),
		('Metroid Prime 3: Corruption', 'Nintendo Wii', '08-27-2007', '90%', GETDATE()),
		('Paper Mario', 'N64', '02-05-2001', '93%', GETDATE()),
		('Paper Mario: The Thousand Year Door', 'GameCube', '10-11-2004', '87%', GETDATE()),
		('Super Paper Mario', 'Nintendo Wii', '04-09-2007', '85%', GETDATE()),
		('Shining Tears', 'PlayStation 2', '03-22-2005', '61%', GETDATE()),
		('Star Ocean: Till The End Of Time', 'PlayStation 2', '08-31-2004', '80%', GETDATE()),
		('Super Mario 64', 'N64', '09-26-1996', '94%', GETDATE()),
		('Super Mario RPG: Legend Of The Seven Stars', 'SNES', '03-09-1996', '93%', GETDATE()),
		('Tales Of Symphonia', 'GameCube', '07-13-2004', '86%', GETDATE()),
		('Tales Of Symphonia: Dawn Of The New World', 'Nintendo Wii', '11-11-2008', '68%', GETDATE()),
		('The Thing', 'PlayStation 2', '08-19-2002', '78%', GETDATE()),
		('Uncharted: Drake''s Fortune', 'PlayStation 3', '11-16-2007', '88%', GETDATE()),
		('Uncharted 2: Among Thieves', 'PlayStation 3', '10-13-2009', '96%', GETDATE()),
		('Uncharted 3: Drake''s Deception', 'PlayStation 3', '11-01-2011', '91%', GETDATE()),
		('Xenogears', 'PlayStation', '10-20-1998', '84%', GETDATE()),
		('XenoSaga: Episode 1', 'PlayStation 2', '02-26-2003', '83%', GETDATE()),
		('XenoSaga: Episode 2', 'PlayStation 2', '02-15-2005', '73%', GETDATE()),
		('XenoSaga: Episode 3', 'PlayStation 2', '08-29-2006', '81%', GETDATE()),
		('Zone Of The Enders', 'PlayStation 2', '03-26-2001', '78%', GETDATE()),
		('Zone Of The Enders: The Second Runner', 'PlayStation 2', '03-10-2003', '82%', GETDATE())
	END
	GO

	EXEC PopulateFullGameListTbl
	GO