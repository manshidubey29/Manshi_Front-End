# Steeleye
1st question-
In programming, the simple List component is a data structure that stores a sequence of elements, typically of the same data type. The elements can be added, removed, or accessed in a specific order. The list is a fundamental data structure used in many programming languages to implement algorithms and data processing.

2nd question-
(a)In the SingleListItem component, onClickHandler prop is marked as required but is not being passed to the component. Instead, onClickHandler(index) is being passed which will immediately call the function when the component is rendered. It should be changed to onClick={() => onClickHandler(index)} to pass the function as a callback.
(b)The isSelected prop in the SingleListItem component is expected to be a boolean but is being assigned the selectedIndex state variable. This variable holds the index of the selected item and should be compared with the current item's index to determine whether it is selected or not. The correct expression should be isSelected={selectedIndex === index}.
(c)In the WrappedListComponent component, the items prop is marked as an array of objects with a text property but is defined as an array of objects with no properties in the default props. It should be defined as an empty array instead of null to avoid errors when accessing properties of items in the component.
(c)The PropTypes.shapeOf() function does not exist. Instead, PropTypes.shape() should be used to define an object with specific properties.
(d)The PropTypes.array() function is being used incorrectly. It should be PropTypes.arrayOf() to define an array of a specific type.

3rd question-
import React, { useState, useEffect, memo } from 'react';
import PropTypes from 'prop-types';

// Single List Item
const WrappedSingleListItem = ({
  index,
  isSelected,
  onClickHandler,
  text,
}) => {
  return (
    <li
      style={{ backgroundColor: isSelected ? 'green' : 'red'}}
      onClick={() => onClickHandler(index)}
    >
      {text}
    </li>
  );
};

WrappedSingleListItem.propTypes = {
  index: PropTypes.number,
  isSelected: PropTypes.bool,
  onClickHandler: PropTypes.func.isRequired,
  text: PropTypes.string.isRequired,
};

const SingleListItem = memo(WrappedSingleListItem);

// List Component
const WrappedListComponent = ({
  items,
}) => {
  const [selectedIndex, setSelectedIndex] = useState(null);

  useEffect(() => {
    setSelectedIndex(null);
  }, [items]);

  const handleClick = index => {
    setSelectedIndex(index);
  };

  return (
    <ul style={{ textAlign: 'left' }}>
      {items.map((item, index) => (
        <SingleListItem
          onClickHandler={() => handleClick(index)}
          text={item.text}
          index={index}
          isSelected={selectedIndex === index}
          key={index}
        />
      ))}
    </ul>
  );
};

WrappedListComponent.propTypes = {
  items: PropTypes.arrayOf(PropTypes.shape({
    text: PropTypes.string.isRequired,
  })),
};

WrappedListComponent.defaultProps = {
  items: [],
};

const List = memo(WrappedListComponent);

export default List;
