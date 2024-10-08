Factory:
	A place for building things
	Where will be construct things
		code units that lead to creation of objects

Problem:
	If we pass a type of object, I should get an object of the type
		1. MySQL -> MySQLDatabase object
		2. PostgreSQL -> PostgreSQLDatabase object
		3. MongoDB -> MongoDB object

	String typeOfDB = "";

	Database db; // Database is interface

	class DatabaseFactory {
		createDatabaseForType(String type) {
			if (type == "mySQL")
				...
		}
	}

if if-else are a part of logic, then it is not a violation of single responsibility
	The single responsibility of the factory: To construct database of the correct type

Benefits of factory:
Whenever I have an interface for whom there are multiple implementations
I need to select one of those implementations based on value of some variable

**Factory will always return a new object**

		public class TaxCalculator {
			void calculateTax(SalaryDetails salaryDetails, TaxRegime regime) {
				int taxAmount = 0;
				if (regime == TaxRegime.OLD) { // Responsibility - how to calculate tax using old regime
					taxAmount += (salaryDetails.hra * 30) / 100;
					taxAmount += (salaryDetails.basePay * 40) / 100;
				} else { // Responsibility - how to calculate tax using new regime
					taxAmount += (salaryDetails.hra + salaryDetails.basePay * 30) / 100;
				}
				return taxAmount;
			}
		} // We need to change codebase if the way we calculate new and old regimes change

		public class SalaryDetails {
			int hra;
			int basePay;
			int epf;
			int lta;
		}

	1. We might want to do different things based on tax regime at different places
	2. To bring two files into another file, we construct an interface

			public interface TaxCalculationAlgorithm {
				int calculateTax(SalaryDetails salaryDetails);
			}

			// Implementation 1
			public class NewRegimeTaxCalculationAlgorithm implements TaxCalculationAlgorithm {
				@Override
				public int calculateTax(SalaryDetails salaryDetails) {
					return 0;
				}
			}

			// Implementation 2
			public class OldRegimeTaxCalculationAlgorithm implements TaxCalculationAlgorithm {
				@Override
				public int calculateTax(SalaryDetails salaryDetails) {
					return 0;
				}
			}

			// New code

			if (regime == TaxRegime.OLD) {
				taxCalculationAlgorithm = new OldRegimeTaxCalcualtionAlgorithm();
			} else if (regime == TaxRegime.NEW) {
				taxCalculationAlgorithm = new NewRegimeTaxCalcualtionAlgorithm();
			} else {
				throw new IllegalArgumentException();
			}

			return taxCalculationAlgorithm.calculateTax(salaryDetails);

	3. Factory:

			public class TaxCalculationAlgorithmFactory {
				public static TaxCalculationAlgorithm getTaxCalculationAlgorithmForRegime(TaxRegime regime) {
					if (regime == TaxRegime.OLD) {
						return new OldRegimeTaxCalculationAlgorithm();
					} else if (regime == TaxRegime.NEW) {
						return new NewRegimeTaxCalculationAlgorithm();
					} else {
						throw new IllegalArgumentException();
					}
				}

				public static TaxCalculationAlgorithm getNewRegimeTaxCalculator() {
					return new NewRegimeTaxCalculationAlgorithm();
				}

				public static getTaxCalculationAlgorithmForIdentifier(String identifier) {
					return new OldRegimeTaxCalculationAlgorithm();
				}
			}

			// Modified code

			TaxCalculationAlgorithm taxCalculationAlgorithm = TaxCalculationAlgorithmFactory.getTaxCalculationAlgorithmForRegime(regime);
			return taxCalculationAlgorithm.calculateTax(salaryDetails);

		1. Using factory makes us use dependency inversion principle

## Factory Method Design Pattern ##
1. Database class

		Database { // Abstract class
			url
			userName
			password

			connect() // Abstract methods
			test()
			Query createQuery()
			executeQuery()
		}

	1. Subclasses

			MySQLDatabase extends Database {
				Query createQuery()
			}

		1. `Query` can also be abstract class
			1. `createQuery` must return a subclass of query
			2. Example:

					Query q = db.createQuery(); // coding to an interface

				1. An object `MySQLQuery` is returned which extends `Query`
				2. `createQuery` is a factory method
					1. The only purpose of a factory method in a class is to return an object of a particular type
2. Example:

		Database
			createQuery -> Query

								
							MySQLQuery PGSQLQuery MongoDBQuery


	1. To return an object of some other class, we use a factory method inside a class
		1. It does not return an object of the type of the class.
