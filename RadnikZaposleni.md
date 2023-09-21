RADNIKTEST

package testovi;

import static org.junit.Assert.assertTrue;
import static org.junit.jupiter.api.Assertions.*;

import org.junit.jupiter.api.BeforeAll;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

import program.Radnik;

class RadnikTest {
	
	Radnik radnik;
	
	@BeforeAll
	public static void setValues() {
		
	}
	
	@BeforeEach
	void init() {
		radnik = new Radnik("Danilo Korac", 12, 140);
	}
	
	@Test
	public void testSetCenaSata1() {
		int ocekivaniRezultat = 12;
		int stvarniRezultat = radnik.getCenaSata();
		
		assertEquals(ocekivaniRezultat, stvarniRezultat);
		
		
		radnik.setCenaSata(7);
		ocekivaniRezultat = 7;
		stvarniRezultat = radnik.getCenaSata();
		assertEquals(ocekivaniRezultat, stvarniRezultat);
		
			
		
	}

	@Test
	public void testSetCenaSata2() {
		int cenaSata = -8;
		assertThrows(RuntimeException.class, () -> radnik.setCenaSata(cenaSata));
		
	}
	
	@Test
	public void testSetBrSatiRada1() {
		int ocekivaniRezultat = 140;
		int stvarniRezultat = radnik.getBrSatiRada();
		
		assertEquals(ocekivaniRezultat, stvarniRezultat);
		
		
		radnik.setBrSatiRada(220);
		ocekivaniRezultat = 220;
		stvarniRezultat = radnik.getBrSatiRada();
		assertEquals(ocekivaniRezultat, stvarniRezultat);		
		
	}
	
	@Test
	void testSetBrSatiRada2() {
		int brSatiRada = -50;
		assertThrows(RuntimeException.class, () -> radnik.setBrSatiRada(brSatiRada));
		
	}
	
	@Test
	void testSetBrSatiRada3() {
		int brSatiRada = 420;
		assertThrows(RuntimeException.class, () -> radnik.setBrSatiRada(brSatiRada));
		
	}
	
	@Test
	public void testSetIme() {
		String ocekivaniRezultat = "Danilo Korac";
		String stvarniRezultat = radnik.getIme();
		
		assertEquals(ocekivaniRezultat, stvarniRezultat);
		
		
		radnik.setIme("Ivan");
		ocekivaniRezultat = "Ivan";
		stvarniRezultat = radnik.getIme();
		assertEquals(ocekivaniRezultat, stvarniRezultat);
		
			
		
	}
	
	@Test
	void testSetIme2() {
		String ime = null;
		assertThrows(RuntimeException.class, () -> radnik.setIme(ime));
		
	}
	
	@Test
	public void testBolovanjeFalse() {
		assertFalse(radnik.bolovanje());
		
	}
	
	@Test
	public void testBolovanjeTrue() {
		radnik.setCenaSata(0);
		assertTrue(radnik.bolovanje());
		
	}
	

}
===============================================================================================================

RADNIKTESTS

package testovi;

import static org.junit.jupiter.api.Assertions.*;

import org.junit.jupiter.api.Test;
import org.junit.platform.runner.JUnitPlatform;
import org.junit.platform.suite.api.SelectClasses;
import org.junit.runner.RunWith;

@RunWith(JUnitPlatform.class)
@SelectClasses(RadnikTest.class)
class RadnikTests {

}

=============================================================================================================

TESTRUNNER

package testovi;


import java.util.logging.Logger;
import org.junit.runner.JUnitCore;
import org.junit.runner.notification.Failure;


class TestRunner {

	public static void main(String[] args) {
		
		org.junit.runner.Result result = JUnitCore.runClasses(RadnikTests.class, ZaposleniTests.class);

        Logger l = Logger.getLogger(TestRunner.class.toString());

        for(Failure f : result.getFailures()){
            l.warning(f.toString());
        }

        l.info("Vreme izvrsavanja: " + result.getRunTime());
        l.info("Ukupan broj izvrsavanja: " + result.getRunCount());

        l.info("Broj uspesno izvrsenih testova: " + (result.getRunCount() - result.getFailureCount() - result.getIgnoreCount() ));
        l.info("Broj palih testova: " + result.getFailureCount());
        l.info("Broj preskocenih testova: " + result.getIgnoreCount());
        l.info("Broj dinamicki preskocenih testova: " + result.getAssumptionFailureCount());

        if(result.wasSuccessful()){
            l.info("Svi testovi su uspesno izvrseni");
        } else {
            l.info("Postoje greske u testovina");
	}
}
	
}

=========================================================================================================================================================

ZAPOSLENITEST

package testovi;

import static org.junit.jupiter.api.Assertions.*;

import java.util.Arrays;
import java.util.Collection;
import java.util.LinkedList;
import java.util.stream.Stream;

import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.BeforeAll;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.Arguments;
import org.junit.jupiter.params.provider.MethodSource;

import program.Radnik;
import program.Zaposleni;

class ZaposleniTest {

	Zaposleni zaposleni;
	Radnik radnik;
	
	public static LinkedList<Radnik> novaLista = new LinkedList<Radnik>();
	@BeforeAll
	public static void create() {
		Zaposleni zaposle = new Zaposleni();
		assertTrue(System.getProperty("os.name").contains("Windows"));
		Zaposleni.radnik.add(new Radnik("Danilo", 12, 120));
	}
	@BeforeEach
	void init() {
		//
	}
	
	@AfterEach
	void destroy() {
		zaposleni = null;
	}
	
	@ParameterizedTest
	@MethodSource("testRadnikDodaj")
	public void testDodajRadnika(Radnik rad) {
		if(rad == null)
		assertThrows(NullPointerException.class, 
				() -> Zaposleni.dodajRadnik(rad));
		else if(Zaposleni.radnik.contains(rad))
			assertThrows(RuntimeException.class, 
					() -> Zaposleni.dodajRadnik(rad));
		else
			Zaposleni.dodajRadnik(rad);
		
	}
	
	public static Collection<Object[]> testRadnikDodaj(){
        return Arrays.asList(new Object[][]{
                {null},
                {new Radnik("Nenad Penezic", 14, 130)},
                {new Radnik("Nenad Penezic", 14, 130)},
                {new Radnik("Danilo Korac", 12, 160)},
                {new Radnik("Ivan Krstic", 18, 100)},
                {new Radnik("Jovan Govedarica", 10, 200)}

        });
        
	}
	
	@ParameterizedTest
	@MethodSource("radnikaPronadji")
	public void testPronadjiRadnika(String ime, int ocekivaniRezultat) {
		if(ime == null)
			assertNull(Zaposleni.pronadjiRadnik(ime));
		else
			assertEquals(ocekivaniRezultat, Zaposleni.pronadjiRadnik(ime).size());
		
	}
	
	public static Stream<Arguments> radnikaPronadji(){
		return Stream.of(
				Arguments.of(null, 0),
				Arguments.of("Marko", 0),
				Arguments.of("Nenad", 0),
				Arguments.of("Danilo", 1));
				
	}
	
}

===================================================================================================================

ZAPOSLENITESTS

package testovi;

import static org.junit.jupiter.api.Assertions.*;

import org.junit.jupiter.api.Test;
import org.junit.platform.runner.JUnitPlatform;
import org.junit.platform.suite.api.SelectClasses;
import org.junit.runner.RunWith;

@RunWith(JUnitPlatform.class)
@SelectClasses(ZaposleniTest.class)
class ZaposleniTests {

}
