TESTPRIZMA

package testovi;

import static org.junit.Assert.*;

import org.junit.Assume;
import org.junit.Before;
import org.junit.BeforeClass;
import org.junit.Rule;
import org.junit.Test;
import org.junit.rules.TestName;
import org.junit.rules.TestRule;
import org.junit.rules.Timeout;

import geometrija.Prizma;

public class TestPrizma {
	
	public Prizma P;
	
	@Rule
	public final TestRule timeout = Timeout.seconds(0);
	
	@Rule
	public final TestName name = new TestName();
	
	@Before
	public void init() {
		P = new Prizma(5, 5, 5);
	}
	
	@BeforeClass
	public static void ProveraOperativnogSistema() {
		Assume.assumeTrue(System.getProperty("os.name").contains("Windows"));
	}

	@Test(expected = RuntimeException.class)
	public void testSetVisina() {
		assertEquals("testSetVisina", name.getMethodName());
		
		int ocekivaniRez = 5;
		int stvarniRez = P.getVisina();
		
		assertEquals(ocekivaniRez, stvarniRez);
		P.setVisina(-1);
	}
	
	@Test
	public void testSetVisina1() {
		assertEquals("testSetVisina1", name.getMethodName());
		
		int ocekivaniRez = 5;
		int stvarniRez = P.getVisina();
		
		assertEquals(ocekivaniRez, stvarniRez);
		P.setVisina(6);
		ocekivaniRez = 6;
		stvarniRez = P.getVisina();
		assertEquals(ocekivaniRez, stvarniRez);
	}

	@Test
	public void testSetSirina() {
		int ocekivaniRez = 5;
		int stvarniRez = P.getSirina();
		
		assertEquals(ocekivaniRez, stvarniRez);
		try {
		P.setSirina(-1);
		}catch(Throwable e){
			Assume.assumeNoException(e);
		}
	}
	
	@Test
	public void testSetSirina1() {
		int ocekivaniRez = 5;
		int stvarniRez = P.getSirina();
		
		assertEquals(ocekivaniRez, stvarniRez);
		P.setSirina(6);
		ocekivaniRez = 6;
		stvarniRez = P.getSirina();
		assertEquals(ocekivaniRez, stvarniRez);
	}

	@Test(expected = RuntimeException.class)
	public void testSetDuzina() {
		int ocekivaniRez = 5;
		int stvarniRez = P.getDuzina();
		
		assertEquals(ocekivaniRez, stvarniRez);
		P.setDuzina(-1);
	}
	
	@Test
	public void testSetDuzina1() {
		int ocekivaniRez = 5;
		int stvarniRez = P.getDuzina();
		
		assertEquals(ocekivaniRez, stvarniRez);
		P.setDuzina(7);
		ocekivaniRez = 7;
		stvarniRez = P.getDuzina();
		assertEquals(ocekivaniRez, stvarniRez);
	}

	@Test
	public void testGetDuzina() {
		int ocekivaniRez = 5;
		int stvarniRez = P.getDuzina();
		
		assertEquals(ocekivaniRez, stvarniRez);
	}

	@Test
	public void testGetSirina() {
		int ocekivaniRez = 5;
		int stvarniRez = P.getSirina();
		
		assertEquals(ocekivaniRez, stvarniRez);
	}
	
	@Test
	public void testGetVisina() {
		int ocekivaniRez = 5;
		int stvarniRez = P.getVisina();
		
		assertEquals(ocekivaniRez, stvarniRez);
	}

	@Test
	public void testZapremina() {
		double ocekivaniRez = (P.getVisina() * P.getSirina() * P.getSirina()/3);
		double stvarniRez = P.zapremina();
		
		assertEquals(ocekivaniRez, stvarniRez,0.001);
	}

	@Test
	public void testVecaOdSto() {
		assertFalse(P.vecaOdSto());
	}
	
	@Test
	public void testVecaOdSto1() {
		P.setSirina(10);
		P.setVisina(10);
		assertTrue(P.vecaOdSto());
	}

	@Test
	public void testToString() {
		String ocekivaniRez = "Prizma [Duzina =" + P.getDuzina()+ ", sirina =" + P.getSirina() + ", visina =" + P.getVisina()+ "]";
		String stvarniRez = P.toString();
		
		assertEquals(ocekivaniRez, stvarniRez);
	}

}


========================================================================================================================================

TESTSPRIZMA

package testovi;

import static org.junit.Assert.*;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.Suite;
import org.junit.runners.Suite.SuiteClasses;

@RunWith(Suite.class)
@SuiteClasses(TestPrizma.class)

public class TestsPrizma {

	
}


==========================================================================================================================================

TESTSLISTAPRIZMI

package testovi;

import static org.junit.Assert.*;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.Suite;
import org.junit.runners.Suite.SuiteClasses;

@RunWith(Suite.class)
@SuiteClasses({TestListaPrizmiDodajPrizmuParametrized.class,TestListaPrizmiPrizmaIZadateGodineParametrizedTest.class})

public class TestsListaPrizmi {

}

===========================================================================================================================================

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
		
		Result result = JUnitCore.runClasses(TestPrizma.class,TestsListaPrizmi.class);
		
		Logger l = Logger.getLogger(TestRunner.class.toString());
		
		for(Failure f:result.getFailures()) {
			l.warning(f.toString());
		}
		
		l.info("Vreme:"+ result.getRunTime());
		l.info("Broj izvrsenih:"+ result.getRunCount());
		l.info("Broj izvrsenih:"+ (result.getRunCount() - result.getFailureCount() - result.getIgnoreCount() - result.getAssumptionFailureCount()));
		l.info("Pali:"+ result.getFailureCount());
		l.info("Ignorisani:"+ result.getIgnoreCount());
		l.info("Dinamicki preskoceni:"+ result.getAssumptionFailureCount());
		
		if(result.wasSuccessful())
			l.info("USPESNO");
		else
			l.warning("NIJE USPESNO");
	}
}


=========================================================================================================================================

TESTLISTAPRIZMIDODAJPRIZMUPARAMETRIZED

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

import geometrija.ListaPrizmi;
import geometrija.Prizma;
@RunWith(Parameterized.class)
public class TestListaPrizmiDodajPrizmuParametrized {
	
	public Prizma P;
	public ListaPrizmi LP;
	
	@Rule
	public final TestRule timeout = Timeout.seconds(6);
	
	@Before
	public void init() {
		LP = new ListaPrizmi();
	}
	
	@BeforeClass
	public static void ProveraOperativnogSistema() {
		Assume.assumeTrue(System.getProperty("os.name").contains("Windows"));
	}
	
	public TestListaPrizmiDodajPrizmuParametrized(Prizma P) {
		this.P=P;
	}
	
	@Parameters
	public static Collection<Object[]> geometrija(){
		return Arrays.asList(new Object[][]{
			{new Prizma(1, 5, 5)},
			{new Prizma(2, 5, 5)},
			{new Prizma(4, 5, 5)},
			{new Prizma(3, 5, 5)},
			{new Prizma(7, 5, 5)},
			{new Prizma(7, 7, 7)}
		});
	}

	@Test(expected = NullPointerException.class)
	public void testDodajPrizma() {
		P = null;
		LP.dodajPrizma(P);
		
	}
	
	@Test(expected = RuntimeException.class)
	public void testDodajPrizma1() {
		LP.dodajPrizma(P);
		LP.dodajPrizma(P);
	}
	
	@Test
	public void testDodajPrizma2() {
		assertFalse(LP.geometrija.contains(P));
		
		LP.dodajPrizma(P);
		assertTrue(LP.geometrija.contains(P));
		
	}
	
	@After
	public void destroy() {
		LP = null;
	}
}

=============================================================================================================================================

TESTLISTAPRIZMIPRIZMAIZADATEGODINEPARAMETRIZED

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
import org.junit.runners.Parameterized.Parameters;

import geometrija.ListaPrizmi;
import geometrija.Prizma;

public class TestListaPrizmiPrizmaIZadateGodineParametrizedTest {
	
	public Prizma P;
	public ListaPrizmi LP;
	
	@Rule
	public final TestRule timeout = Timeout.seconds(6);
	
	@Before
	public void init() {
		LP = new ListaPrizmi();
	}
	
	@BeforeClass
	public static void ProveraOperativnogSistema() {
		Assume.assumeTrue(System.getProperty("os.name").contains("Windows"));
	}
	
	public TestListaPrizmiPrizmaIZadateGodineParametrizedTest(Prizma P) {
		this.P=P;
	}
	
	@Parameters
	public static Collection<Object[]> geometrija(){
		return Arrays.asList(new Object[][] {
			{new Prizma(5, 5, 5)},
			{new Prizma(5, 5, 5)},
			{new Prizma(5, 5, 5)},
			{new Prizma(5, 5, 5)},
			{new Prizma(5, 5, 5)},
			{new Prizma(5, 5, 5)},
		});
	}

	@Test
	public void testPrizmaiZadateGodine() {
		double zap = 0;
		LP.PrizmaiZadateGodine(zap);
	}
	
	@Test
	public void testPrizmaiZadateGodine1() {
	assertFalse(LP.geometrija.contains(P));
	LP.dodajPrizma(P);
	LinkedList<Prizma> geometrija=new LinkedList<Prizma>();
	geometrija.add(P);
	assertEquals(geometrija, LP.PrizmaiZadateGodine(5));
	}
	
	@Test
	public void testPrizmaiZadateGodine2() {
		assertFalse(LP.geometrija.contains(P));
		LP.dodajPrizma(P);
		LinkedList<Prizma> prizme = new LinkedList<Prizma>();
		prizme.add(P);
		assertNotEquals(prizme, LP.PrizmaiZadateGodine(5));
		
	}
	
	@After
	public void destroy() {
		LP = null;
	}
}
