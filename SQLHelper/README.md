# SQLHelper
## Wichtiges vorweg
Das Projekt ist nicht fertig. Es dient lediglich dem Zweck, zu verstehen, wie man mit Datenbanken kommuniziert.

## Was ist das und welches Ziel hat das Projekt
Das Ziel dieses Projekts ist es, eine Verbindung zu einer beliebigen SQL Datenbank aufzubauen.

## Bisher unterstütze Datenbanken
1. MySQL
2. MsSQL

## Beispiel
```javascript
	// ungetestet
	
	public enum DATABASE_TYPE {
	    MsSQL, MySQL;
	}
	
	private SqlHelper sqlHelper = null;
	private String host,database,user,passwd;
	// for MsSQL only
	private boolean winlogon = false;
	// MySQL as standard database
	private DATABASE_TYPE type = DATABASE_TYPE.MySQL;
	
	public static void main(String[] args) {
		host = ""; database = ""; user =""; passwd="";
		createSqlHelper();
		// query with result in form: List<String[]>
		List<String[]> result = sqlHelper.executeSQLQuery("SELECT BEFEHL");
		
		// query without result (such as Inserts)
		sqlHelper.executeSQLQueryWithoutResult("INSERT ...");
	}
	
	/**
	 * creates MsSqlHelper class and tests connection
	 * 
	 * @return MsSqlHelper object if connection test succeeded but null if not  
	 */
	private MsSqlHelper makeMsSqlHelper() {
		MsSqlHelper mssql = new MsSqlHelper(host, database, user, passwd, winlogon);
		try {
			if(mssql.testConnection())
				return mssql;
		} catch (SQLException e) {
			System.out.println(SqlHelper.printSQLException(e));
		}
		return null;
	}
	
	/**
	 * creates MySqlHelper class and tests connection
	 * 
	 * @return MySqlHelper object if connection test succeeded but null if not  
	 */
	private MySqlHelper makeMySqlHelper() {
		MySqlHelper mysql = new MySqlHelper(host, database, user, passwd);
		try {
			if(mysql.testConnection())
				return mysql;
		} catch (SQLException e) {
			System.out.println(SqlHelper.printSQLException(e));
		}
		return null;
	}
	
	/**
	 * creates specified db helper
	 */
	private void createSqlHelper() {
		switch(type) {
		case MySQL:
			this.sqlHelper = this.makeMySqlHelper();
			break;
		case MsSQL:
			this.sqlHelper = this.makeMsSqlHelper();
			break;
		default:
			this.sqlHelper = null;
			break;
		}
	}
``` 

Wenn das noch nicht reicht, schaut euch ein anderes Projekt von mir an (github.com/incredibleXE/DB2Prak2)


### Microsoft SQL Server
Wenn ihr versucht mit dem Microsoft SQL Datenbankserver zu reden, gibt es noch die Möglichkeit die Authentifikation über die integrierte Windowsanmeldung aufzubauen. Um das zu aktivieren, müsst ihr noch folgenden Code anpassen.
```javascript
MsSqlHelper mssql = new MsSqlHelper(host, database, user, passwd, true);
```
Damit diese Authentifikationsart funktioniert, müsst ihr jedoch noch die "ntlmauth.dll" aus dem ordner "lib/EURE_ARCHITEKTUR/SSO/" in den Java lib Ordner kopieren.
#### für 32 Bit Java 7 jre
```
lib/i868/SSO/ntlmauth.dll -> C:\Program Files (x86)\Java\jre7\lib\i386
```
#### für 64 Bit Java 7 jre
```
lib/amd64/SSO/ntlmauth.dll -> C:\Program Files\Java\jre7\lib\amd64
```

#### für 32 Bit Java 8 jre
```
lib/i868/SSO/ntlmauth.dll -> C:\Program Files (x86)\jre1.8.0_25\jre7\lib\i386
```
#### für 64 Bit Java 8 jre
```
lib/amd64/SSO/ntlmauth.dll -> C:\Program Files\Java\jre1.8.0_25\lib\amd64
```

## Lizenz
Meinen Namen erwähnen wäre schön. Verwenden könnt ihr es wie ihr wollt.

## Kontakt
Wenn ihr fragen habt, schreibt mich einfach an:
[incrediblexe92@gmail.com](mailto:incrediblexe92@gmail.com)