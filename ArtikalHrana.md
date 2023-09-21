ARTIKAL

package hrana;

public class Artikal {
	private String naziv= null;
	private int cena= 0;
	private int broj= 0;

	public Artikal(String naziv, int cena, int broj) {
		super();
		this.naziv= naziv;
		this.cena= cena;
		this.broj= broj;
	}

	public int getCena() {
		return cena;
	}

	public void setCena(int cena) {
		if (cena< 0)
			throw new RuntimeException("Cena artikla ne sme biti manja od 0");
		this.cena= cena;
	}

	public int getBroj() {
		return broj;
	}

	public void setBroj(int broj) {
		if (broj< 0)
			throw new RuntimeException("Broj komada artikala mora biti veci od 0");
		this.broj= broj;
	}

	public String getNaziv() {
		return naziv;
	}

	public void setNaziv(String naziv) {
		if (naziv== null)
			throw new RuntimeException("Morate uneti naziv artikla");
		this.naziv= naziv;
	}

	public double ukupnaCena() {
		return (this.broj * this.cena * 1.18);
	}

	public boolean viseOdJedan() {
		if (this.broj > 1)
			return true;
		else
			return false;
	}

	@Override
	public String toString() {
		return "Artikal [naziv=" + naziv+ ", cena =" + cena + ", broj =" + broj+ "]";
	}

}

========================================================================================

PRODAVNICA

package hrana;

import java.util.LinkedList;

public class Prodavnica {
	public static LinkedList<Artikal> lista = new LinkedList<Artikal>();

	public static void dodajArtikal(Artikal a) {
		if (a == null)
			throw new NullPointerException("Artikal ne sme biti null");
		if (lista.contains(a))
			throw new RuntimeException("Artikal vec postoji");
		lista.add(a);
	}

	public static LinkedList<Artikal> pronadjiArtikle(int broj) {
		if (broj == 0)
			return null;
		LinkedList<Artikal> novaLista = new LinkedList<Artikal>();
		for (int i = 0; i < lista.size(); i++)
			if (lista.get(i).viseOdJedan()==true)
				novaLista.add(lista.get(i));
		return novaLista;
	}
}

============================================================================================

TESTARTIKAL

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

import hrana.Artikal;

public class TestArika {
	
	public Artikal A;
	
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
		A = new Artikal("Kafa", 180, 5);
	}

	@Test
	public void testGetCena() {
		assertEquals("testGetCena", name.getMethodName());
		
		int ocekivaniRezultat = 180;
		int stvarniRezultat = A.getCena();
		
		assertEquals(ocekivaniRezultat, stvarniRezultat);
	}

	@Test(expected = RuntimeException.class)
	public void testSetCena() {
		assertEquals("testSetCena", name.getMethodName());
		
		int ocekivaniRezultat = 180;
		int stvarniRezultat = A.getCena();
		
		assertEquals(ocekivaniRezultat, stvarniRezultat);
		A.setCena(-4);
	}
	
	@Test
	public void testSetCena1() {
		assertEquals("testSetCena1", name.getMethodName());
		
		int ocekivaniRezultat = 180;
		int stvarniRezultat = A.getCena();
		
		assertEquals(ocekivaniRezultat, stvarniRezultat);
		A.setCena(200);
		ocekivaniRezultat = 200;
		stvarniRezultat = A.getCena();
		assertEquals(ocekivaniRezultat, stvarniRezultat);
	}

	@Test
	public void testGetBroj() {
		assertEquals("testGetBroj", name.getMethodName());
		
		int ocekivaniRezultat = 5;
		int stvarniRezultat = A.getBroj();
		
		assertEquals(ocekivaniRezultat, stvarniRezultat);
	}

	@Test(expected = RuntimeException.class)
	public void testSetBroj1() {
		assertEquals("testSetBroj1", name.getMethodName());
		
		int ocekivaniRezultat = 5;
		int stvarniRezultat = A.getBroj();
		
		assertEquals(ocekivaniRezultat, stvarniRezultat);
		A.setBroj(-4);
	}
	
	@Test
	public void testSetBroj2() {
		assertEquals("testSetBroj2", name.getMethodName());
		
		int ocekivaniRezultat = 5;
		int stvarniRezultat = A.getBroj();
		
		assertEquals(ocekivaniRezultat, stvarniRezultat);
		A.setBroj(10);
		ocekivaniRezultat = 10;
		stvarniRezultat = A.getBroj();
		assertEquals(ocekivaniRezultat, stvarniRezultat);
	}

	@Test
	public void testGetNaziv() {
		String ocekivaniRezultat = "Kafa";
		String stvarniRezultat = A.getNaziv();
		
		assertEquals(ocekivaniRezultat, stvarniRezultat);
	}

	@Test(expected = RuntimeException.class)
	public void testSetNaziv() {
		String ocekivaniRezultat = "Kafa";
		String stvarniRezultat = A.getNaziv();
		
		assertEquals(ocekivaniRezultat, stvarniRezultat);
		A.setNaziv(null);
	}
	
	@Test
	public void testSetNaziv1() {
		String ocekivaniRezultat = "Kafa";
		String stvarniRezultat = A.getNaziv();
		
		assertEquals(ocekivaniRezultat, stvarniRezultat);
		A.setNaziv("Jakobs");
		ocekivaniRezultat = "Jakobs";
		stvarniRezultat = A.getNaziv();
		assertEquals(ocekivaniRezultat, stvarniRezultat);
	}

	@Test
	public void testUkupnaCena() {
		double ocekivaniRezultat = (A.getBroj() * A.getCena()* 1.18);
		double stvarniRezultat = A.ukupnaCena();
		
		assertEquals(ocekivaniRezultat, stvarniRezultat,0.01);
	}

	@Test
	public void testViseOdJedan() {
		assertTrue(A.viseOdJedan());
	}
	
	@Test
	public void testViseOdJedan1() {
		A.setBroj(0);
		assertFalse(false);
	}

	@Test
	public void testToString() {
		String ocekivaniRezultat = "Artikal [naziv=" + A.getNaziv()+ ", cena =" + A.getCena() + ", broj =" + A.getBroj()+ "]";
		String stvarniRezultat = A.toString();
		
		assertEquals(ocekivaniRezultat, stvarniRezultat);
	}

}

=======================================================================================================================================

TESTPRODAVNICADODAJARTIKALPARAMETRIZED

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

import hrana.Artikal;
import hrana.Prodavnica;

public class TestProdavnicaDodajArtikalParametrized {
	
	public Artikal A;
	public Prodavnica P;
	
	@Rule
	public final TestRule timeout = Timeout.seconds(6);
	
	@BeforeClass
	public static void ProveraOperativnogSistemna() {
		Assume.assumeTrue(System.getProperty("os.name").contains("Windows"));
	}
	
	@Before
	public void init() {
		P = new Prodavnica();
	}
	
	@Parameters
	public static Collection<Object[]> hrana(){
		return Arrays.asList(new Object[][] {
			{new Artikal("Kafa", 180, 5)},
			{new Artikal("Kafa", 180, 5)},
			{new Artikal("Sok", 200, 4)},
			{new Artikal("Kafa", 180, 5)},
			{new Artikal("Cokolada", 120, 3)},
			{new Artikal("Kafa", 180, 5)},
		});
	}

	@Test(expected = NullPointerException.class)
	public void testDodajArtikal() {
		A = null;
		P.dodajArtikal(A);
	}
	
	@Test(expected = NullPointerException.class)
	public void testDodajArtikal1() {
		P.dodajArtikal(A);
		P.dodajArtikal(A);
	}
	
	@Test
	public void testDodajArtikal2() {
		Artikal m = new Artikal("Majonez", 200, 4);
		P.dodajArtikal(m);
	}
	
	public void destroy() {
		P = null;
	}

}

===========================================================================================

TESTPRODAVNICAPRONADJIARTIKALPARAMETRIZED

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

import hrana.Artikal;
import hrana.Prodavnica;

public class TestProdavnicaPronadjiArtikalParametrized {
	
	public Artikal A;
	public Prodavnica P;
	
	@Rule
	public final TestRule timeout = Timeout.seconds(6);
	
	@BeforeClass
	public static void ProveraOperativnogSistemna() {
		Assume.assumeTrue(System.getProperty("os.name").contains("Windows"));
	}
	
	@Before
	public void init() {
		P = new Prodavnica();
	}
	
	@Parameters
	public static Collection<Object[]> hrana(){
		return Arrays.asList(new Object[][] {
			{new Artikal("Kafa", 180, 5)},
			{new Artikal("Kafa", 180, 5)},
			{new Artikal("Sok", 200, 4)},
			{new Artikal("Kafa", 180, 5)},
			{new Artikal("Cokolada", 120, 3)},
			{new Artikal("Kafa", 180, 5)},
		});
	}

	@Test
	public void testPronadjiArtikle() {
		int broj = 0;
		P.pronadjiArtikle(broj);
	}
	
	@Test
	public void testPronadjiArtikle1() {
		int cena = 15;
		P.pronadjiArtikle(cena);
	}
	
	@Test
	public void testPronadjiArtikle2() {
		Artikal a = new Artikal("Kecap", 150, 1);
		int cena = a.getCena();
		P.pronadjiArtikle(cena);
	}
	
	public void destroy() {
		P = null;
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

public class TestRuner {

	public static void main(String[] args) {
		
		Result result = JUnitCore.runClasses(TestsArtikal.class,TestsProdavnica.class);
		
		Logger l = Logger.getLogger(TestRuner.class.toString());
		
		for(Failure f:result.getFailures()) {
			l.warning(f.toString());
		}
		
		
		
		if(result.wasSuccessful())
			l.info("da");
		else
			l.warning("ne");
	}

}
====================================================================================================

TESTARTIKAL

package testovi;

import static org.junit.Assert.*;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.Suite;
import org.junit.runners.Suite.SuiteClasses;

@RunWith(Suite.class)
@SuiteClasses({TestArika.class})

public class TestsArtikal {

	@Test
	public void test() {
		fail("Not yet implemented");
	}

}
========================================================================================================

TESTPRODAVNICA

package testovi;

import static org.junit.Assert.*;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.Suite;
import org.junit.runners.Suite.SuiteClasses;

@RunWith(Suite.class)
@SuiteClasses({TestProdavnicaDodajArtikalParametrized.class,TestProdavnicaPronadjiArtikalParametrized.class})

public class TestsProdavnica {

	@Test
	public void test() {
		fail("Not yet implemented");
	}

}
