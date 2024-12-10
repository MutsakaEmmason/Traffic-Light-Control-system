#include <avr/io.h>
#include <avr/interrupt.h>
#include <util/delay.h>

// Define ultrasonic sensor pins
#define TRIG_PIN 8
#define ECHO_PIN 9

void uart_init() {
    UBRR0H = 0;
    UBRR0L = 103; // 9600 baud rate
    UCSR0B = (1 << TXEN0); // Enable TX
    UCSR0C = (1 << UCSZ01) | (1 << UCSZ00); // 8-bit data
}

void uart_send(char data) {
    while (!(UCSR0A & (1 << UDRE0))); // Wait until buffer is empty
    UDR0 = data;
}

uint16_t measure_distance() {
    // Send a pulse to trigger the ultrasonic sensor
    PORTB |= (1 << PB0); // Set Trigger HIGH
    _delay_us(10);
    PORTB &= ~(1 << PB0); // Set Trigger LOW

    while (!(PINB & (1 << PB1))); // Wait for Echo HIGH
    TCNT1 = 0; // Reset timer
    TCCR1B |= (1 << CS11); // Start timer
    while (PINB & (1 << PB1)); // Wait for Echo LOW
    TCCR1B = 0; // Stop timer

    return TCNT1 / 58; // Convert timer value to cm
}

int main() {
    DDRB |= (1 << PB0); // Set Trigger Pin as Output
    DDRB &= ~(1 << PB1); // Set Echo Pin as Input
    uart_init();

    while (1) {
        uint16_t distance = measure_distance();
        if (distance < 20) {
            uart_send('O'); // Obstacle detected
        } else {
            uart_send('C'); // No obstacle
        }
        _delay_ms(500);
    }
}
