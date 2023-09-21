AUTOGUMATEST

package testovi;

import static org.junit.Assert.*;

import org.junit.Assume;
import org.junit.Before;
import org.junit.BeforeClass;
import org.junit.Rule;
import org.junit.Test;
import org.junit.rules.ErrorCollector;
import org.junit.rules.ExpectedException;
import org.junit.rules.TestName;
import org.junit.rules.TestRule;
import org.junit.rules.Timeout;

import gume.AutoGuma;
import gume.VulkanizerskaRadnja;

public class AutoGumaTest {

	public AutoGuma AG;

	@Rule
	public final TestRule timeout = Timeout.seconds(5);

	@BeforeClass
	public static void ProveriOperativniSistem() {
		Assume.assumeTrue(System.getProperty("os.name").contains("Windows"));
	}

	@Rule
	public final ErrorCollector ec = new ErrorCollector();

	@Before
	public void init() {
		AG = new AutoGuma("Michelin", true, 18, 180, 40);
	}

	@Rule
	public final TestName name = new TestName();

	@Test
	public void getZimskaTest() {
		try {
			assertEquals("getZimskaTest", name.getMethodName());
		} catch (Throwable t) {
			ec.addError(t);
		}

		boolean ocekivaniRezultat = true;

		try {
			boolean stvarniRezultat = AG.getZimska();
			assertEquals(ocekivaniRezultat, stvarniRezultat);
		} catch (Throwable t) {
			ec.addError(t);
		}
	}

	@Test
	public void setZimskaTest() {
		assertEquals("setZimskaTest", name.getMethodName());
		boolean ocekivaniRezultat = true;
		boolean stvarniRezultat = AG.getZimska();
		try {
			assertEquals(ocekivaniRezultat, stvarniRezultat);
		} catch (Throwable t) {
			ec.addError(t);
		}

		AG.setZimska(false);
		ocekivaniRezultat = false;
		stvarniRezultat = AG.getZimska();
		try {
			assertEquals(ocekivaniRezultat, stvarniRezultat);
		} catch (Throwable t) {
			ec.addError(t);
		}
	}

	@Test(expected = RuntimeException.class)
	public void setPrecnikTest() {
		int ocekivaniRezultat = 18;
		int stvarniRezultat = AG.getPrecnik();
		assertEquals(ocekivaniRezultat, stvarniRezultat);

		AG.setPrecnik(10);
	}

	@Test(expected = RuntimeException.class)
	public void setPrecnikTest2() {
		int ocekivaniRezultat = 18;
		int stvarniRezultat = AG.getPrecnik();
		assertEquals(ocekivaniRezultat, stvarniRezultat);

		AG.setPrecnik(25);
	}

	@Test
	public void setPrecnikTest3() {
		int ocekivaniRezultat = 18;
		int stvarniRezultat = AG.getPrecnik();
		try {
			assertEquals(ocekivaniRezultat, stvarniRezultat);
		} catch (Throwable t) {
			ec.addError(t);
		}

		AG.setPrecnik(15);
		ocekivaniRezultat = 15;
		stvarniRezultat = AG.getPrecnik();
		try {
			assertEquals(ocekivaniRezultat, stvarniRezultat);
		} catch (Throwable t) {
			ec.addError(t);
		}

	}

	@Rule
	public ExpectedException exception = ExpectedException.none();

	@Test
	public void setSirinaTest() {
		exception.expect(RuntimeException.class);
		exception.expectMessage("Sirina van opsega");
		int ocekivaniRezultat = 180;
		int stvarniRezultat = AG.getSirina();
		assertEquals(ocekivaniRezultat, stvarniRezultat);

		AG.setSirina(120);
	}

	@Test
	public void setSirinaTest2() {
		exception.expect(RuntimeException.class);
		exception.expectMessage("Sirina van opsega");
		int ocekivaniRezultat = 180;
		int stvarniRezultat = AG.getSirina();
		assertEquals(ocekivaniRezultat, stvarniRezultat);

		AG.setSirina(360);
	}

	@Test
	public void setSirinaTest3() {
		int ocekivaniRezultat = 180;
		int stvarniRezultat = AG.getSirina();
		assertEquals(ocekivaniRezultat, stvarniRezultat);

		AG.setSirina(250);
		ocekivaniRezultat = 250;
		stvarniRezultat = AG.getSirina();
		assertEquals(ocekivaniRezultat, stvarniRezultat);
	}

	@Test
	public void setVisinaTest() {

		int ocekivaniRezultat = 40;
		int stvarniRezultat = AG.getVisina();
		assertEquals(ocekivaniRezultat, stvarniRezultat);

		try {
			AG.setVisina(20);
		} catch (Throwable t) {
			Assume.assumeNoException(t);
		}
	}

	@Test
	public void setVisinaTest2() {

		int ocekivaniRezultat = 40;
		int stvarniRezultat = AG.getVisina();
		assertEquals(ocekivaniRezultat, stvarniRezultat);

		try {
			AG.setVisina(100);
		} catch (Throwable t) {
			Assume.assumeNoException(t);
		}
	}

	@Test
	public void setVisinaTest3() {

		int ocekivaniRezultat = 40;
		int stvarniRezultat = AG.getVisina();
		assertEquals(ocekivaniRezultat, stvarniRezultat);

		AG.setVisina(50);
		ocekivaniRezultat = 50;
		stvarniRezultat = AG.getVisina();
		assertEquals(ocekivaniRezultat, stvarniRezultat);
	}

	@Test
	public void getMarkaModelTest() {
		String ocekivaniRezultat = "Michelin";
		String stvarniRezultat = AG.getMarkaModel();
		assertEquals(ocekivaniRezultat, stvarniRezultat);
	}

	@Test(expected = RuntimeException.class)
	public void setMarkaModelTest() {
		String ocekivaniRezultat = "Michelin";
		String stvarniRezultat = AG.getMarkaModel();
		assertEquals(ocekivaniRezultat, stvarniRezultat);

		AG.setMarkaModel(null);
	}

	@Test(expected = RuntimeException.class)
	public void setMarkaModelTest2() {
		String ocekivaniRezultat = "Michelin";
		String stvarniRezultat = AG.getMarkaModel();
		assertEquals(ocekivaniRezultat, stvarniRezultat);

		AG.setMarkaModel("A1");
	}

	@Test
	public void setMarkaModelTest3() {
		String ocekivaniRezultat = "Michelin";
		String stvarniRezultat = AG.getMarkaModel();
		assertEquals(ocekivaniRezultat, stvarniRezultat);

		AG.setMarkaModel("Pirelli");
		ocekivaniRezultat = "Pirelli";
		stvarniRezultat = AG.getMarkaModel();
		assertEquals(ocekivaniRezultat, stvarniRezultat);
	}

	@Test
	public void izracunajCenuTest() {
		double ocekivaniRezultat = (AG.getPrecnik() * 3 + AG.getSirina() + AG.getVisina()) * 28.53;
		double stvarniRezultat = AG.izracunajCenu();
		assertEquals(ocekivaniRezultat, stvarniRezultat, 0.001);
	}

	@Test
	public void povoljnaGuma() {
		assertFalse(AG.povoljnaGuma());
	}

	@Test
	public void povoljnaGuma2() {
		AG.setSirina(135);
		AG.setPrecnik(13);
		AG.setVisina(25);
		assertTrue(AG.povoljnaGuma());
	}

	@Test
	public void toStringTest() {
		String ocekivaniRezultat = "AutoGuma [markaModel=" + AG.getMarkaModel() + ", precnik=" + AG.getPrecnik()
				+ ", sirina=" + AG.getSirina() + ", visina=" + AG.getVisina() + "]";
		String stvarniRezultat = AG.toString();
		assertEquals(ocekivaniRezultat, stvarniRezultat);
	}
	
	@Test
	public void equalsTest1() {
		AutoGuma AG2 = new AutoGuma("Michelin", true, 18, 180, 40);
		assertTrue(AG.equals(AG2));
	}
	@Test
	public void equalsTest2() {
		VulkanizerskaRadnja VK = new VulkanizerskaRadnja();
		assertEquals(false, AG.equals(VK));
	}
	@Test
	public void equalsTest3() {
		AutoGuma AG2 = AG;
		assertTrue(AG.equals(AG2));
	}
	@Test
	public void equalsTest4() {
		AutoGuma AG2 = new AutoGuma(null, true, 18, 180, 40);
		assertFalse(AG.equals(AG2));
	}
	@Test
	public void equalsTest5() {
		AutoGuma AG2 = new AutoGuma(null, true, 18, 180, 40);
		AutoGuma AG3 = new AutoGuma(null, true, 18, 180, 40);
		assertTrue(AG2.equals(AG3));
	}
	@Test
	public void equalsTest6() {
		AutoGuma AG2 = new AutoGuma(null, true, 18, 180, 40);
		AutoGuma AG3 = new AutoGuma("Michelin", true, 18, 180, 40);
		assertFalse(AG2.equals(AG3));
	}
	@Test
	public void equalsTest7() {
		AutoGuma AG2 = new AutoGuma("Michelin", true, 19, 180, 40);
		assertFalse(AG.equals(AG2));
	}
	@Test
	public void equalsTest8() {
		AutoGuma AG2 = new AutoGuma("Michelin", true, 18, 185, 40);
		assertFalse(AG.equals(AG2));
	}
	@Test
	public void equalsTest9() {
		AutoGuma AG2 = new AutoGuma("Michelin", true, 18, 180, 35);
		assertFalse(AG.equals(AG2));
	}
}

===========================================================================================================

AUTOGUMATESTS

package testovi;

import org.junit.runner.RunWith;
import org.junit.runners.Suite;
import org.junit.runners.Suite.SuiteClasses;

@RunWith(Suite.class)
@SuiteClasses({ AutoGumaTest.class })
public class AutoGumaTests {

}

==============================================================================================================

VRPARAMETRIZEDTESTS

package testovi;

import org.junit.runner.RunWith;
import org.junit.runners.Suite;
import org.junit.runners.Suite.SuiteClasses;

@RunWith(Suite.class)
@SuiteClasses({ VulkanizerskaRadnjaDodajGumuParametrizedTest.class,
		VulkanizerskaRadnjaPronadjiGumuParazmetrizedTest.class })
public class VRParametrizedTests {

}

==================================================================================================================

VULKANIZERSKARADNJADODAJGUMUPARAMETRIZED

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

import gume.AutoGuma;
import gume.VulkanizerskaRadnja;

@RunWith(Parameterized.class)
public class VulkanizerskaRadnjaDodajGumuParametrizedTest {

	private AutoGuma AG;
	private VulkanizerskaRadnja VR;
	
	@BeforeClass
	public static void ProveriOperativniSistem() {
		Assume.assumeTrue(System.getProperty("os.name").contains("Windows"));
	}
	
	@Rule
	public final TestRule timeout = Timeout.seconds(5);

	public VulkanizerskaRadnjaDodajGumuParametrizedTest(AutoGuma AG) {
		this.AG = AG;
	}

	@Parameters
	public static Collection<Object[]> gume() {
		return Arrays.asList(new Object[][] {
			{new AutoGuma("Michelin", true, 18, 180, 40)},
			{new AutoGuma("Michelin", true, 18, 180, 40)},
			{new AutoGuma("Michelin", true, 18, 180, 40)},
			{new AutoGuma("Pireli", false, 19,170, 30)}
		});
	}
	
	@Before
	public void init() {
		VR = new VulkanizerskaRadnja();
	}

	@Test(expected = NullPointerException.class)
	public void dodajGumuTest() {
		AG = null;
		VR.dodajGumu(AG);
	}

	@Test(expected = RuntimeException.class)
	public void dodajGumuTest2() {
		VR.dodajGumu(AG);
		VR.dodajGumu(AG);
	}

	@Test
	public void dodajGumuTest3() {
		assertFalse(VR.gume.contains(AG));
		VR.dodajGumu(AG);
		assertTrue(VR.gume.contains(AG));
	}
	
	@After
	public void destroy() {
		VR = null;
	}

}

====================================================================================================================

VULKANIZERSKARADNJAPRONADJIGUMUPARAMETRIZED

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

import gume.AutoGuma;
import gume.VulkanizerskaRadnja;

@RunWith(Parameterized.class)
public class VulkanizerskaRadnjaPronadjiGumuParazmetrizedTest {

	private AutoGuma AG;
	private VulkanizerskaRadnja VR;
	
	@BeforeClass
	public static void ProveriOperativniSistem() {
		Assume.assumeTrue(System.getProperty("os.name").contains("Windows"));
	}
	
	@Rule
	public final TestRule timeout = Timeout.seconds(5);

	public VulkanizerskaRadnjaPronadjiGumuParazmetrizedTest(AutoGuma AG) {
		this.AG = AG;
	}

	@Parameters
	public static Collection<Object[]> gume() {
		return Arrays.asList(new Object[][] {
			{new AutoGuma("Michelin", true, 18, 180, 40)},
			{new AutoGuma("Michelin", true, 18, 185, 45)},
			{new AutoGuma("Michelin", true, 18, 190, 40)},
			{new AutoGuma("Michelin", false, 19,170, 30)}
		});
	}
	
	@Before
	public void init() {
		VR = new VulkanizerskaRadnja();
	}

	@Test
	public void dodajGumuTest() {
		String marka = null;
		assertNull(VR.pronadjiGumu(marka));
	}

	@Test
	public void dodajGumuTest2() {
		assertFalse(VR.gume.contains(AG));
		VR.dodajGumu(AG);
		LinkedList<AutoGuma> gume = new LinkedList<AutoGuma>();
		gume.add(AG);
		assertEquals(gume, VR.pronadjiGumu("Michelin"));
	}
	
	@Test
	public void dodajGumuTest3() {
		assertFalse(VR.gume.contains(AG));
		VR.dodajGumu(AG);
		LinkedList<AutoGuma> gumes = new LinkedList<AutoGuma>();
		gumes.add(AG);
		assertNotEquals(gumes, VR.pronadjiGumu("Pireli - NotExistingModel"));
	}
	
	@After
	public void destroy() {
		VR = null;
	}

}

====================================================================================================================

TESTRUNNER

package testovi;

import java.util.logging.Logger;

import org.junit.runner.JUnitCore;
import org.junit.runner.Result;
import org.junit.runner.notification.Failure;

public class TestRunner {

	public static void main(String[] args) {
		Result result = JUnitCore.runClasses(AutoGumaTests.class, VRParametrizedTests.class);
		
		Logger l = Logger.getLogger(TestRunner.class.toString());
		
		for (Failure f: result.getFailures()) {
			l.warning(f.toString());
		}
		
		l.info("Vreme izvrsavanja:" + result.getRunTime());
		l.info("Broj testova:"+ result.getRunCount());
		
		l.info("Uspesno testova:" + (result.getRunCount()-result.getFailureCount()-result.getIgnoreCount()-result.getAssumptionFailureCount()));
		l.info("Broj palih testova:"+ result.getFailureCount());
		l.info("Broj preskocenih:"+ result.getIgnoreCount());
		l.info("Broj dinamicki preskocenih:" + result.getAssumptionFailureCount());
		
		if (result.wasSuccessful()) 
			l.info("Svi testovi su uspesno izvrseni");
		else
			l.warning("Postoje greske u testovima");

	}

}
