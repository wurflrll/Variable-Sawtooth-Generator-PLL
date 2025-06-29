For another project I needed to generate variable frequency and amplitude sawtooth waveforms. Initially what I wanted was to make a small personal function
generator and interface for an 8-ohm speaker just for fun.  In the process I was thinking about having multiple channels, and in particular what if I wanted
to generate an additional sawtooth with given phase difference but identical frequency.  This I decided was enough for it's own PCB.  There are three reference 
signals: amplitude, frequency, and phase offset.  The circuit is analog and made out of discrete components, but an ESP32 & DAC is included if the user doesn't want 
to generate reference signals externally. The phase reference works by resetting channel 2 when channel 1 is equal to the phase reference.  The tricky part
is that the frequency of the two signals are determined by their 2 RC time constants.  I wanted the slope of channel 2 to match the slope of channel 1
irrespective of component tolerances (and for example without relying on example a small tolerance shunt resistor).  This circuit taught me a lot about 
hysteresis and the whole circuit is just one op-amp feedback circuit inside of another.  An LTSpice simulation file will be added as well.

The three ref signals:

Amplitude (AMP_REF): Identically determines amplitude (eg. 3V input creates 3V amplitude of Sawtooth)

Frequency (FREQ_REF): The FREQ_ref signals actually determines the slope of the sawtooth, where 1V input = 2V/millisecond slope
So the frequency equation is simply Frequency (in kHz) = 2 * FREQ / AMP_REF

Phase Offset: The phase offset is simply 360 degrees * PHASE_REF/AMP_REF (ie. frequency)

                    
