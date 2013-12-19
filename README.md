EWSJavaAPI
==========
* fork from http://archive.msdn.microsoft.com/ewsjavaapi
* add gradle script


Example send mail
=================
```
	String ewsurl = "https://localhost/EWS/Exchange.asmx";
	String user = "my@test.com";
	String password = "PASSWORD FOR LOGIN EXCHANGE";
	String testmail = "other@test.com";

	ExchangeService service = new ExchangeService(ExchangeVersion.Exchange2010);
	ExchangeCredentials credentials = new WebCredentials(user, password);
	service.setCredentials(credentials);
	try {
		service.setUrl(new URI(ewsurl));

		EmailMessage msg = new EmailMessage(service);
		msg.setSubject("Hello world!");
		msg.setBody(MessageBody.getMessageBodyFromText("Sent using the EWS Managed API."));
		msg.getToRecipients().add(testmail);
		msg.send();
	} catch (Exception e) {
		e.printStackTrace();
	}
```


Example send appointment
=================
```
	String ewsurl = "https://localhost/EWS/Exchange.asmx";
	String user = "my@test.com";
	String password = "PASSWORD FOR LOGIN EXCHANGE";
	String testmail = "other@test.com";

	ExchangeService service = new ExchangeService(ExchangeVersion.Exchange2010);
	ExchangeCredentials credentials = new WebCredentials(user, password);
	service.setCredentials(credentials);
	try {
		service.setUrl(new URI(ewsurl));

		SimpleDateFormat formatter = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
		Appointment appointment = new Appointment(service);
		appointment.setSubject("Recurrence Appointment for JAVA XML TEST");
		appointment.setBody(MessageBody.getMessageBodyFromText("Recurrence Test Body Msg"));
		appointment.setStart(formatter.parse("2013-12-19 12:00:00"));
		appointment.setEnd(formatter.parse("2013-12-19 13:00:00"));
		appointment.getRequiredAttendees().add(testmail);
		appointment.save();
	} catch (Exception e) {
		e.printStackTrace();
	}
```
