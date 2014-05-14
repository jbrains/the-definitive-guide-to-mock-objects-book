In 2014 I read an article with the provocative title ["Mockists are Dead. Long live Classicists."](#ref-mockists-are-dead). In it, the author frames mock objects as "dangerous" and warns against a mistake he calls "tautological TDD", which he describes as writing tests that repeat an idea in different words. This sounds risky to me, and something I'd probably want to warn against. I wondered how mock objects could create this problem, then I examined his example.[^ref-ttdd-example]

[^ref-ttdd-example]: Fabio Pereira, ["TTDD - Tautological Test Driven Development (Anti Pattern)"](http://link.jbrains.ca/RE9DUO)

The example centers around a `CarRepository`, which appears to implement the [Domain-Driven Design](#ref-domain-driven-design) Repository pattern in a straightforward way. The production code looks like this:

```
public class CarRepository {
  private ServiceHeaderFactory serviceHeaderFactory;
  private CarService carService;

  public CarRepository(ServiceHeaderFactory serviceHeaderFactory,
                    CarService carService) {
    this.serviceHeaderFactory = serviceHeaderFactory;
    this.carService = carService;
  }
  public Cars findAll() {
    ServiceHeader serviceHeader = serviceHeaderFactory.create();
    return carService.findAll(serviceHeader);
  }
}
```

The test looks like this:

```
@Test
public void shouldRetrieveCarsFromCarServiceUsingTheRightServiceHeader() throws Exception {
  // GIVEN
  ServiceHeader serviceHeader = new ServiceHeader();
  ServiceHeaderFactory serviceHeaderFactoryMock = mock(ServiceHeaderFactory.class);
  when(serviceHeaderFactoryMock.create()).thenReturn(serviceHeader);
  CarService carServiceMock = mock(CarService.class);
  CarRepository carRepository = new CarRepository(serviceHeaderFactoryMock, carServiceMock);

  // WHEN
  carRepository.findAll();

  // THEN
  verify(carServiceMock).findAll(serviceHeader);
}
```

The author calls this test "tautological" because the checks appear only to duplicate the implementation. I agree: the **when** and **then** lines...

* `when(serviceHeaderFactoryMock.create()).thenReturn(serviceHeader)`
* `verify(carServiceMock).findAll(serviceHeader)`

...correspond perfectly to a couple of lines in the production code.

* `ServiceHeader serviceHeader = serviceHeaderFactory.create()`
* `return carService.findAll(serviceHeader)`

From this, the author reasons that the test provides no useful information, categorises it as redundant, labels it "tautological", and considers it dangerous. He writes:

> When we write tests this way, most of the time if the implementation changes, we end up changing the expectations of the test as well and yeah, the tests pass automagically. But without knowing much about its **behaviour**. These tests are a mirror of the implementation, therefore tautological.&mdash;Fabio Pereira

## Another Interpretation

I understand the author's perspective, and I remember feeling skeptical about this myself. It felt strange seeing this correspondence, and it seemed like the same thing every time: the expectation at the end of my test corresponded to the last line of my production method, and the stubs corresponded to almost every other line of the method. I thought that this must fly in the face of *Don't Repeat Yourself*, *Once and Only Once*, and *The Four Elements of Simple Design*, and that made me nervous.

Let me offer another way to interpret the situation. Some objects interact very, very simply with their collaborators. Some objects act as simple mediators: .... It seems pretty reasonable to me that the checks for a mediator of only two collaborators with a single code path would look too simple. I don't think of this as a consequence of using mock objects, but rather a consequence of a very simple design. **I consider this a good thing**. Next month, when we discover that this mediator needs to do more, I suspect that I'll find it easy to understand and easy to add new behavior.

## What Do We Really Have Here?

I don't like way the author has checked the `CarRepository`, because it obscures the important part of the code. Why does this repository exist? I can see two possibilities:

* It adapts the `CarService` to the `CarRepository` interface.
* It interprets "all cars" to mean "all cars with a default service header".

How I proceed depends on this interpretation.

***NYI***


