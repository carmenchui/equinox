.NOTPARALLEL:

#-- Variables

INST    = ../instantiate
OBJS    = $(INST)/MiniSatInstantiateClause.o $(INST)/MiniSatWrapper.o
HFLAGS  = -fglasgow-exts -O2 -threaded
HSAT    = -lstdc++ -I../instantiate $(OBJS)
GHC     = ghc

#-- Main

ifeq ($(OS),Windows_NT)
	EXE=.exe
else
	EXE=
endif

main: ../paradox$(EXE) ../equinox$(EXE) ../infinox$(EXE)


Sat.o: Sat.hs
	$(GHC) -fglasgow-exts --make Sat.hs

#-- EquiParadox

#equiparadox$(EXE): Sat.o *.hs Paradox/*.hs Equinox/*.hs EquiParadox/*.hs ../instantiate/*.or ../minisat/current-base/*.or
#	$(GHC) $(HSAT) $(HFLAGS) -main-is EquiParadox.Main.main --make EquiParadox.Main -o equiparadox

#-- Paradox

../paradox$(EXE): Sat.o *.hs Paradox/*.hs ../instantiate/*.o
	$(GHC) $(HSAT) $(HFLAGS) --make Paradox/Main.hs -o ../paradox

../smellyparadox$(EXE): Sat.o *.hs Paradox/*.hs ../instantiate/*.o
	$(GHC) $(HSAT) $(HFLAGS) -main-is Paradox.Smelly.main --make Paradox.Smelly -o ../smellyparadox

#-- Equinox

../equinox$(EXE): Sat.o *.hs Equinox/*.hs ../instantiate/*.o
	$(GHC) $(HSAT) $(HFLAGS) -threaded --make Equinox/Main.hs -o ../equinox

#-- Infinox

../infinox$(EXE): *.hs Infinox/*.hs
	$(GHC) $(HFLAGS) -main-is Infinox.Main.main --make Infinox.Main -o ../infinox


#-- SatPlay

../satplay$(EXE): Sat.o *.hs ../instantiate/*.o
	$(GHC) $(HSAT) $(HFLAGS) -main-is SatPlay.Main.main --make SatPlay.Main -o ../satplay

../smellysox$(EXE): Sat.o SmellySox/*.hs SmellySox/Parser/Partff.hs ../instantiate/*.o
	$(GHC) $(HSAT) $(HFLAGS) --make SmellySox/Main -o ../smellysox

SmellySox/Parser/Partff.hs: SmellySox/tff.cf
	bnfc -p SmellySox.Parser SmellySox/tff.cf
	alex SmellySox/Parser/Lextff.x
	happy SmellySox/Parser/Partff.y

#-- Zoomer

../zoomer$(EXE): Sat.o *.hs ../instantiate/*.o
	$(GHC) $(HSAT) $(HFLAGS) -main-is Zoomer.Main.main --make Zoomer.Main -o ../zoomer

#-- Cleaning up

clean:
	rm -f *.o *.hi paradox* equinox* infinox* satplay* Equinox/*.o Equinox/*.hi Paradox/*.o Paradox/*.hi Infinox/*.o Infinox/*.hi SatPlay/*.o SatPlay/*.hi


