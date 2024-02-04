###### Create a LocalDate instance representing the current date.

LocalDate today = LocalDate.now();

###### Create a LocalTime instance representing the current time.

LocalTime now = LocalTime.now();

###### Create a LocalDateTime instance representing the current date and time.
LocalDateTime nowDateTime = LocalDateTime.now();

###### Create a ZonedDateTime instance representing the current date and time in the UTC time zone.
ZonedDateTime nowZonedDateTime = ZonedDateTime.now(ZoneOffset.UTC);

###### Parse a string into a LocalDate instance.
LocalDate birthday = LocalDate.parse("1990-01-01");

###### Format a LocalDate instance into a string.
String formattedBirthday = birthday.format(DateTimeFormatter.ISO_LOCAL_DATE);

###### Add one day to a LocalDate instance.
LocalDate tomorrow = today.plusDays(1);

###### Subtract one month from a LocalDate instance.
LocalDate lastMonth = today.minusMonths(1);

###### Check if a LocalDate instance is before another LocalDate instance.
boolean isBefore = today.isBefore(tomorrow);

###### Check if a LocalDate instance is after another LocalDate instance.
boolean isAfter = today.isAfter(yesterday);

###### Check if a LocalDate instance is equal to another LocalDate instance.
boolean isEqual = today.isEqual(tomorrow);
