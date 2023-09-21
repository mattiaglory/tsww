FILM

package film;

public class Film {
	private String naslov = null;
	private int trajanje = 0;
	private int brGledalaca = 0;

	public Film(String naslov, int trajanje, int brGledalaca) {
		super();
		this.naslov = naslov;
		this.trajanje = trajanje;
		this.brGledalaca = brGledalaca;
	}

	public int getTrajanje() {
		return trajanje;
	}

	public void setTrajanje(int trajanje) {
		if (trajanje < 0)
			throw new RuntimeException("Trajanjene sme biti manja od 0");
		this.trajanje = trajanje;
	}

	public int getBrGledalaca() {
		return brGledalaca;
	}

	public void setBrGledalaca(int brGledalaca) {
		if (brGledalaca < 0)
			throw new RuntimeException("Broj gledalaca mora biti veca od 0 ");
		this.brGledalaca = brGledalaca;
	}

	public String getNaslov() {
		return naslov;
	}

	public void setNaslov(String naslov) {
		if (naslov == null)
			throw new RuntimeException("Morate uneti naslov ");
		this.naslov = naslov;
	}

	public double izracunajHonorar() {
		return (this.brGledalaca * 200);
	}

	public boolean neuspesanFilm() {
		if (this.izracunajHonorar() <= 100000)
			return true;
		else
			return false;
	}
}

=====================================================================================================

PRODUKCIJAFILMA

package film;

import java.util.LinkedList;

public class ProdukcijaFilm {
	public  LinkedList<Film> film = new LinkedList<Film>();

	public  void dodajFilm(Film a) {
		if (a == null)
			throw new NullPointerException("Film ne sme biti null");
		if (film.contains(a))
			throw new RuntimeException("Film vec postoji");
		film.add(a);
	}

	public  LinkedList<Film> pronadjiFilm(String naslov) {
		if (naslov == null)
			return null;
		LinkedList<Film> novaLista = new LinkedList<Film>();
		for (int i = 0; i < film.size(); i++)
			if (film.get(i).getNaslov().equals(naslov))
				novaLista.add(film.get(i));
		return novaLista;
	}
}

==================================================================================================

TESTFILM

package testovi;

import static org.junit.Assert.*;

import org.junit.Assume;
import org.junit.Before;
import org.junit.BeforeClass;
import org.junit.Rule;
import org.junit.Test;
import org.junit.rules.ErrorCollector;
import org.junit.rules.TestName;
import org.junit.rules.TestRule;
import org.junit.rules.Timeout;

import film.Film;

public class TestFilm {
	
	public Film F;
	
	@Rule
	public final TestRule timeout = Timeout.seconds(6);
	
	@Rule
	public final TestName name = new TestName();
	
	@Rule
	public final ErrorCollector ec = new ErrorCollector();
	
	@BeforeClass
	public static void ProveraOperativnogSistema() {
		Assume.assumeTrue(System.getProperty("os.name").contains("Windows"));
	}

	@Before
	public void init() {
		F = new Film("Loopers", 2, 1000);
	}
	
	@Test
	public void testGetTrajanje() {
		assertEquals("testGetTrajanje", name.getMethodName());
		
		int ocekivaniRez = 2;
		int stvarniRez = F.getTrajanje();
		
		assertEquals(ocekivaniRez, stvarniRez);
	}

	@Test(expected = RuntimeException.class)
	public void testSetTrajanje() {
		assertEquals("testSetTrajanje", name.getMethodName());
		
		int ocekivaniRez = 2;
		int stvarniRez = F.getTrajanje();
		
		assertEquals(ocekivaniRez, stvarniRez);
		
		F.setTrajanje(-1);
	}
	
	@Test
	public void testSetTrajanje1() {
		assertEquals("testSetTrajanje1", name.getMethodName());
		
		int ocekivaniRez = 2;
		int stvarniRez = F.getTrajanje();
		
		assertEquals(ocekivaniRez, stvarniRez);
		
		F.setTrajanje(3);
		ocekivaniRez = 3;
		stvarniRez = F.getTrajanje();
		
		assertEquals(ocekivaniRez, stvarniRez);
	}

	@Test
	public void testGetBrGledalaca() {
		assertEquals("testGetBrGledalaca", name.getMethodName());
		
		int ocekivaniRez = 1000;
		int stvarniRez = F.getBrGledalaca();
		
		assertEquals(ocekivaniRez, stvarniRez);
	}

	@Test
	public void testSetBrGledalaca() {
		assertEquals("testSetBrGledalaca", name.getMethodName());
		
		int ocekivaniRez = 1000;
		int stvarniRez = F.getBrGledalaca();
		
		assertEquals(ocekivaniRez, stvarniRez);
		try {
		F.setBrGledalaca(-1);
		}catch(Throwable t) {
			Assume.assumeNoException(t);
		}
		
	}

	@Test
	public void testGetNaslov() {
		try {
		assertEquals("testGetNaslov", name.getMethodName());
		}catch(Throwable t) {
			ec.addError(t);
		}
		
		String ocekivaniRez = "Loopers";
		String stvarniRez = F.getNaslov();
		
		assertEquals(ocekivaniRez, stvarniRez);
	}

	@Test(expected = RuntimeException.class)
	public void testSetNaslov() {
		try {
			assertEquals("testSetNaslov", name.getMethodName());
			}catch(Throwable t) {
				ec.addError(t);
			}
			
			String ocekivaniRez = "Loopers";
			String stvarniRez = F.getNaslov();
			
			assertEquals(ocekivaniRez, stvarniRez);
			
			F.setNaslov(null);
	}
	
	@Test
	public void testSetNaslov1() {
		try {
			assertEquals("testSetNaslov1", name.getMethodName());
			}catch(Throwable t) {
				ec.addError(t);
			}
			
			String ocekivaniRez = "Loopers";
			String stvarniRez = F.getNaslov();
			
			assertEquals(ocekivaniRez, stvarniRez);
			
			F.setNaslov("Loopers 1");
			ocekivaniRez = "Loopers 1";
			stvarniRez = F.getNaslov();
			
			assertEquals(ocekivaniRez, stvarniRez);
	}

	@Test
	public void testIzracunajHonorar() {
		double ocekivaniRez = (F.getBrGledalaca() * 200);
		double stvarniRez = F.izracunajHonorar();
		
		assertEquals(ocekivaniRez, stvarniRez,0.001);
	}

	@Test
	public void testNeuspesanFilm() {
		assertFalse(F.neuspesanFilm());
	}
	
	@Test
	public void testNeuspesanFilm1() {
		F.setBrGledalaca(10);
		assertTrue(F.neuspesanFilm());
	}


}

=====================================================================================

TESTPRODUKCIJAFILMDODAJFILMPARAMETRIZEDTEST

package testovi;

import static org.junit.Assert.*;

import java.util.Arrays;
import java.util.Collection;

import org.junit.After;
import org.junit.Assume;
import org.junit.Before;
import org.junit.BeforeClass;
import org.junit.Rule;
import org.junit.Test;
import org.junit.rules.TestRule;
import org.junit.rules.Timeout;
import org.junit.runner.RunWith;
import org.junit.runners.Parameterized;
import org.junit.runners.Parameterized.Parameters;

import film.Film;
import film.ProdukcijaFilm;

@RunWith(Parameterized.class)
public class TestProdukcijaFilmDodajFilmParametrizedTest {
	
	public Film F;
	public ProdukcijaFilm PF;
	
	public TestProdukcijaFilmDodajFilmParametrizedTest(Film F) {
		this.F = F;
	}
	
	@Rule
	public final TestRule timeout = Timeout.seconds(6);
	
	@Before
	public void init() {
		PF = new ProdukcijaFilm();
	}
	
	@BeforeClass
	public static void ProveraOperativnogSistema() {
		Assume.assumeTrue(System.getProperty("os.name").contains("Windows"));
	}
	@Parameters
	public static Collection<Object[]> film(){
		return Arrays.asList(new Object[][] {
				{new Film("Loopers", 2, 1000)},
				{new Film("Loopers", 2, 1000)},
				{new Film("Loopers", 2, 1000)},
				{new Film("Loopers", 2, 1000)}
		});
	}
	@Test(expected = NullPointerException.class)
	public void testDodajFilm() {
		F = null;
		PF.dodajFilm(F);
	}
	
	@Test(expected = RuntimeException.class)
	public void testDodajFilm1() {
		PF.dodajFilm(F);
		PF.dodajFilm(F);
	}
	
	@Test
	public void testDodajFilm2() {
		assertFalse(PF.film.contains(F));
		PF.dodajFilm(F);
		assertTrue(PF.film.contains(F));
	}
	
	@After
	public void destroy() {
		PF = null;
	}
}

===============================================================================================

TESTPRODUKCIJAFILMPRONADJIFILMPARAMETRIZEDTEST

package testovi;
import static org.junit.Assert.*;

import java.util.Arrays;
import java.util.Collection;
import java.util.LinkedList;

import org.junit.After;
import org.junit.Assume;
import org.junit.Before;
import org.junit.BeforeClass;
import org.junit.Rule;
import org.junit.Test;
import org.junit.rules.TestRule;
import org.junit.rules.Timeout;
import org.junit.runner.RunWith;
import org.junit.runners.Parameterized;
import org.junit.runners.Parameterized.Parameters;

import film.Film;
import film.ProdukcijaFilm;

@RunWith(Parameterized.class)
public class TestProdukcijaFilmPronadjiFilmParametrizedTest {
	public Film F;
	public ProdukcijaFilm PF;
	public TestProdukcijaFilmPronadjiFilmParametrizedTest(Film F) {
		this.F = F;
	}
	
	@Rule
	public final TestRule timeout = Timeout.seconds(6);
	
	@Before
	public void init() {
		PF = new ProdukcijaFilm();
	}
	
	@BeforeClass
	public static void ProveraOperativnogSistema() {
		Assume.assumeTrue(System.getProperty("os.name").contains("Windows"));
	}
	@Parameters
	public static Collection<Object[]> film(){
		return Arrays.asList(new Object[][] {
				{new Film("Loopers", 2, 1000)},
				{new Film("Loopers", 2, 1000)},
				{new Film("Loopers", 2, 1000)},
				{new Film("Loopers", 2, 1000)}
		});
	}
	@Test
	public void testPronadjiFilm() {
		String naslov = null;
		PF.pronadjiFilm(naslov);
	}
	@Test
	public void testPronadjiFilm1() {
		assertFalse(PF.film.contains(F));
		PF.dodajFilm(F);
		LinkedList<Film> film = new LinkedList<>();
		film.add(F);
		assertEquals(film, PF.pronadjiFilm("Loopers"));
	}
	@Test
	public void testPronadjiFilm2() {
		assertFalse(PF.film.contains(F));
		PF.dodajFilm(F);
		LinkedList<Film> film1 = new LinkedList<>();
		film1.add(F);
		assertNotEquals(film1, PF.pronadjiFilm("Loopers 1"));
	}
	@After
	public void destroy() {
		PF = null;
	}
}

==============================================================================

TESTRUNNER

package testovi;

import static org.junit.Assert.*;

import java.util.logging.Logger;

import org.junit.Test;
import org.junit.runner.JUnitCore;
import org.junit.runner.Result;
import org.junit.runner.notification.Failure;

public class TestRunner {

	public static void main(String[] args) {
		
		Result result = JUnitCore.runClasses(TestsFilm.class,TestsProdukcijaFilm.class);
		
		Logger l = Logger.getLogger(TestRunner.class.toString());
		
		for(Failure f: result.getFailures()) {
			l.warning(f.toString());
		}
		
		l.info("Vreme:" + result.getRunTime());
		l.info("Broj izvrsenih testova:" + result.getRunCount());
		l.info("Broj uspesno izvrsenih:" + (result.getRunCount() - result.getAssumptionFailureCount() - result.getFailureCount() - result.getIgnoreCount()));
		l.info("Dinamicki preskoceni:" + result.getAssumptionFailureCount());
		
		if(result.wasSuccessful())
			l.info("USPESNO");
		else
			l.warning("NEUSPESNO");
	}

}
=============================================================================================================================================================

TESTFILM

package testovi;

import static org.junit.Assert.*;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.Suite;
import org.junit.runners.Suite.SuiteClasses;

@RunWith(Suite.class)
@SuiteClasses({TestFilm.class})
public class TestsFilm {



}
===========================================================================================================

TESTPRODUKCIJAFILM

package testovi;

import static org.junit.Assert.*;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.Suite;
import org.junit.runners.Suite.SuiteClasses;

@RunWith(Suite.class)
@SuiteClasses({TestProdukcijaFilmDodajFilmParametrizedTest.class,TestProdukcijaFilmPronadjiFilmParametrizedTest.class})
public class TestsProdukcijaFilm {


}
