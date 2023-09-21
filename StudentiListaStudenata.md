TESTSTUDENT

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

import studenti.Student;

public class TestStudent {
	
	public Student S;
	
	@Rule
	public final TestRule timeout = Timeout.seconds(6);
	
	@Rule
	public final TestName name = new TestName();
	
	@BeforeClass
	public static void ProveraOperativnogSistema() {
		Assume.assumeTrue(System.getProperty("os.name").contains("Windows"));
	}
	
	@Before
	public void init() {
		S = new Student("Nikola", 4, 180);
	}

	@Test
	public void testGetGodinaStudija() {
		assertEquals("testGetGodinaStudija", name.getMethodName());
		
		int ocekivaniRez = 4;
		int stvarniRez = S.getGodinaStudija();
		
		assertEquals(ocekivaniRez, stvarniRez);
	}

	@Test(expected = RuntimeException.class)
	public void testSetGodinaStudija() {
		
		int ocekivaniRez = 4;
		int stvarniRez = S.getGodinaStudija();
		
		assertEquals(ocekivaniRez, stvarniRez);
		S.setGodinaStudija(5);
	}
	
	@Test(expected = RuntimeException.class)
	public void testSetGodinaStudija1() {
		
		int ocekivaniRez = 4;
		int stvarniRez = S.getGodinaStudija();
		
		assertEquals(ocekivaniRez, stvarniRez);
		S.setGodinaStudija(-1);
	}
	
	@Test
	public void testSetGodinaStudija2() {
		
		int ocekivaniRez = 4;
		int stvarniRez = S.getGodinaStudija();
		
		assertEquals(ocekivaniRez, stvarniRez);
		S.setGodinaStudija(3);
		
		ocekivaniRez = 3;
		stvarniRez = S.getGodinaStudija();
		assertEquals(ocekivaniRez, stvarniRez);
		
	}

	@Test
	public void testGetBrojESPB() {
		int ocekivaniRez = 180;
		int stvarniRez = S.getBrojESPB();
		
		assertEquals(ocekivaniRez, stvarniRez);
	}

	@Test(expected = RuntimeException.class)
	public void testSetBrojESPB() {
		int ocekivaniRez = 180;
		int stvarniRez = S.getBrojESPB();
		
		assertEquals(ocekivaniRez, stvarniRez);
		S.setBrojESPB(400);
	}
	
	@Test(expected = RuntimeException.class)
	public void testSetBrojESPB1() {
		int ocekivaniRez = 180;
		int stvarniRez = S.getBrojESPB();
		
		assertEquals(ocekivaniRez, stvarniRez);
		S.setBrojESPB(-1);
	}
	
	@Test
	public void testSetBrojESPB2() {
		int ocekivaniRez = 180;
		int stvarniRez = S.getBrojESPB();
		
		assertEquals(ocekivaniRez, stvarniRez);
		S.setBrojESPB(150);
		ocekivaniRez = 150;
		stvarniRez = S.getBrojESPB();
		assertEquals(ocekivaniRez, stvarniRez);
	}

	@Test
	public void testGetImeIPrezime() {
		String ocekivaniRez = "Nikola";
		String stvarniRez = S.getImeIPrezime();
		
		assertEquals(ocekivaniRez, stvarniRez);
	}

	@Test(expected = RuntimeException.class)
	public void testSetImeIPrezime() {
		String ocekivaniRez = "Nikola";
		String stvarniRez = S.getImeIPrezime();
		
		assertEquals(ocekivaniRez, stvarniRez);
		S.setImeIPrezime(null);
	}
	
	@Test
	public void testSetImeIPrezime1() {
		String ocekivaniRez = "Nikola";
		String stvarniRez = S.getImeIPrezime();
		
		assertEquals(ocekivaniRez, stvarniRez);
		S.setImeIPrezime("Milos");
		ocekivaniRez  = "Milos";
		stvarniRez = S.getImeIPrezime();
		assertEquals(ocekivaniRez, stvarniRez);
	}

	@Test
	public void testProsekESPB() {
		double ocekivaniRez = (S.getBrojESPB() / S.getGodinaStudija());
		double stvarniRez = S.prosekESPB();
		
		assertEquals(ocekivaniRez, stvarniRez,0.01);
	}

	@Test
	public void testRedovniDrugaGod() {
		assertFalse(S.redovniDrugaGod());
	}
	
	@Test
	public void testRedovniDrugaGod1() {
		S.setBrojESPB(100);
		assertTrue(S.redovniDrugaGod());
	}

	@Test
	public void testToString() {
		String ocekivaniRez = "Student [ime i prezime=" + S.getImeIPrezime()+ ", godina studija =" + S.getGodinaStudija() + ", broj ESPB =" + S.getBrojESPB()+ "]";
		String stvarniRez = S.toString();
		
		assertEquals(ocekivaniRez, stvarniRez);
	}

}

========================================================================================================================================================================

TESTSSTUDENT

package testovi;

import static org.junit.Assert.*;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.Suite;
import org.junit.runners.Suite.SuiteClasses;

@RunWith(Suite.class)
@SuiteClasses({TestStudent.class})

public class TestsStudent {

	

}

=========================================================================================================================================================================

TESTLISTASTUDENATA

package testovi;

import static org.junit.Assert.*;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.Suite;
import org.junit.runners.Suite.SuiteClasses;

@RunWith(Suite.class)
@SuiteClasses({TestListaStudentDodajStudentParemetrized.class,TestListaStudentStudentiZadateGodineParametrized.class})

public class TestsListaStudent {

	
}

=================================================================================================================================================================================

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
		
		Result result = JUnitCore.runClasses(TestStudent.class,TestsListaStudent.class);
		
		Logger l = Logger.getLogger(TestRunner.class.toString());
		
		for(Failure f:result.getFailures()) {
			l.warning(f.toString());
		}
		
		l.info(""+ result.getRunTime());
		l.info(""+ result.getRunCount());
		
		l.info(""+ (result.getRunCount() - result.getFailureCount() - result.getIgnoreCount() - result.getAssumptionFailureCount()));
		
		if(result.wasSuccessful())
			l.info("USPESNO");
		else
			l.warning("Greska");
		
	}

}
=============================================================================================================================================================================

TESTLISTASTUDENTZADATEGODINEPARAMETRIZED

package testovi;

import static org.junit.Assert.*;

import java.util.Arrays;
import java.util.Collection;

import org.junit.Assume;
import org.junit.Before;
import org.junit.BeforeClass;
import org.junit.Rule;
import org.junit.Test;
import org.junit.rules.TestRule;
import org.junit.rules.Timeout;
import org.junit.runners.Parameterized.Parameters;

import studenti.ListaStudenata;
import studenti.Student;

public class TestListaStudentStudentiZadateGodineParametrized {
	
	public Student S;
	public ListaStudenata LS;
	
	@Rule
	public final TestRule timeout = Timeout.seconds(6);
	
	@Before
	public void init() {
		LS = new ListaStudenata();
	}
	
	@BeforeClass
	public static void ProveraOperativnogSistema() {
		Assume.assumeTrue(System.getProperty("os.name").contains("Windows"));
	}
	
	@Parameters
	public static Collection<Object[]> studenti(){
		return Arrays.asList(new Object[][] {
			{new Student("Ivan", 3, 180) },
			{new Student("Ivan", 3, 180) },
			{new Student("Ivan", 3, 180) },
			{new Student("Ivan", 3, 180) },
			{new Student("Ivan", 3, 180) },
			{new Student("Ivan", 3, 180) },
		});
	}

	@Test
	public void testStudentiZadateGodine() {
		int godina = 0;
		LS.studentiZadateGodine(godina);
	}
	
	@Test
	public void testStudentiZadateGodine1() {
		int godina = 4;
		LS.studentiZadateGodine(godina);
	}
	
	@Test
	public void testStudentiZadateGodine2() {
		int godina = 4;
		LS.studentiZadateGodine(godina);
	}

}

=================================================================================================================

TESTLISTASTUDENATADODAJSTUDENTAPARAMETRIZED

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
import org.junit.runners.Parameterized.Parameters;

import studenti.ListaStudenata;
import studenti.Student;

public class TestListaStudentDodajStudentParemetrized {
	
	public Student S;
	public ListaStudenata LS;
	
	@Rule
	public final TestRule timeout = Timeout.seconds(6);
	
	@Before
	public void init() {
		LS = new ListaStudenata();
	}
	
	@BeforeClass
	public static void ProveraOperativnogSistema() {
		Assume.assumeTrue(System.getProperty("os.name").contains("Windows"));
	}
	
	@Parameters
	public static Collection<Object[]> studenti(){
		return Arrays.asList(new Object[][] {
			{new Student("Ivan", 3, 180) },
			{new Student("Ivan", 3, 180) },
			{new Student("Ivan", 3, 180) },
			{new Student("Ivan", 3, 180) },
			{new Student("Ivan", 3, 180) },
			{new Student("Ivan", 3, 180) },
		});
	}

	@Test(expected = NullPointerException.class)
	public void testDodajStudent() {
		S = null;
		LS.dodajStudent(S);
	}
	
	@Test(expected = RuntimeException.class)
	public void testDodajStudent1() {
		LS.dodajStudent(S);
		LS.dodajStudent(S);
	}
	@Test
	public void testDodajStudent2() {
		Student s = new Student("Lazo", 4, 360);
		LS.dodajStudent(s);	
	}
	@After
	public void destroy() {
		LS = null;
	}

}
